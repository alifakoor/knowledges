---
title: "HashiCorp Vault concepts and architecture"
source: "https://claude.ai/chat/e0fb43f5-e365-4fe9-9baf-590296d5f144"
author:
published:
created: 2026-07-05
description: "Claude conversation with 8 messages"
tags:
  - "clippings"
---
there's a cleaner pattern that fits how you already run things (Docker Compose, GitLab CI health-gated deploys): let **Vault Agent** handle authentication and credential renewal as a sidecar, so your app code doesn't touch Vault at all.

![[vault_agent_sidecar_pattern.svg|697]]

This handles your "sometimes deployed and restarted" reality nicely: whether the container comes up fresh or the process is long-running, the sidecar's job never changes — keep the file current.

### Vault Agent config (the sidecar's job)


```hcl
# agent.hcl
pid_file = "/tmp/pidfile"

auto_auth {
  method "approle" {
    config = {
      role_id_file_path   = "/vault/config/role-id"
      secret_id_file_path = "/vault/config/secret-id"
    }
  }
}

template {
  contents             = <<EOT
{{ with secret "database/creds/mycourt-backend-role" }}
MONGO_URI=mongodb://{{ .Data.username }}:{{ .Data.password }}@mongo:27017/mycourt?authSource=mycourt
{{ end }}
EOT
  destination          = "/vault/secrets/mongo.env"
}
```

Vault Agent re-runs the template automatically whenever the lease is close to expiring — it handles the renew-or-refetch decision internally, so you don't write that logic yourself.

### Compose additions

```yaml
services:
  mongo:
    # ...your existing mongo service, unchanged...

  vault-agent:
    image: hashicorp/vault:1.15
    container_name: vault-agent
    command: ["vault", "agent", "-config=/vault/config/agent.hcl"]
    volumes:
      - ./vault-agent/agent.hcl:/vault/config/agent.hcl:ro
      - ./vault-agent/role-id:/vault/config/role-id:ro
      - ./vault-agent/secret-id:/vault/config/secret-id:ro
      - vault-secrets:/vault/secrets
    networks:
      - saba
    restart: unless-stopped

  nestjs-app:
    build: .
    volumes:
      - vault-secrets:/vault/secrets:ro
    networks:
      - saba
    restart: unless-stopped
    depends_on:
      - vault-agent
      - mongo

volumes:
  vault-secrets:

networks:
  saba:
    external:
      name: saba
```

### NestJS side — just watch a file, no Vault SDK calls

```typescript
import { watch } from 'fs';
import { readFileSync } from 'fs';
import * as dotenv from 'dotenv';

const SECRETS_PATH = '/vault/secrets/mongo.env';

function loadAndConnect() {
  const env = dotenv.parse(readFileSync(SECRETS_PATH));
  mongoose.disconnect().then(() => mongoose.connect(env.MONGO_URI));
}

loadAndConnect(); // on startup
watch(SECRETS_PATH, { persistent: true }, () => loadAndConnect()); // on renewal
```

The upside for your setup specifically: this pattern is identical whether it's `badesaba` or any other project, it survives redeploys with zero app-code changes, and it keeps the Vault-awareness entirely in infra config rather than scattered across services — which fits how you've already structured things like the n8n/Vault AppRole integration.


that's exactly right, and it's worth taking seriously. `role_id` + `secret_id` together are functionally a username + password. Whoever has both can log into Vault and get whatever the attached policy allows — in your case, dynamic MongoDB credentials. AppRole gives you several knobs specifically to shrink that risk. Here's how to actually lock it down.

### 1. Make the secret_id short-lived and single-use

bash

```bash
vault write auth/approle/role/mycourt-backend-role \
  token_policies="mycourt-db-policy" \
  secret_id_ttl="10m" \
  secret_id_num_uses=1 \
  token_ttl="1h" \
  token_max_ttl="4h" \
  token_num_uses=0
```

- `secret_id_ttl=10m` — if it's ever leaked, it's already useless soon after.
- `secret_id_num_uses=1` — it can log in exactly once. This matters more than it sounds: it means a `secret_id` is only ever meant to be consumed at container startup, not stored anywhere long-term. If your Vault Agent tries to use it twice (e.g. container restart), you need a fresh one each time — which pushes you toward the delivery mechanism below.

### 2. Bind it to where it's allowed to come from

bash

```bash
vault write auth/approle/role/mycourt-backend-role \
  secret_id_bound_cidrs="10.0.0.0/24" \
  token_bound_cidrs="10.0.0.0/24"
```

Now even a stolen `role_id`+`secret_id` pair is useless from outside your VM subnet/VPN range. Given you already run WireGuard tunnels between VMs, this is a natural fit — bind the CIDR to your internal overlay network, not the public internet.

### 3. Never let the secret_id sit in a file/image/git long-term — use response wrapping for delivery

The riskiest moment is _handing_ the secret_id to the container. Don't bake it into the image, don't commit it, don't put it in a plain compose `.env` that lives on disk indefinitely. Instead, generate a **wrapped** secret_id at deploy time from your GitLab CI pipeline:

bash

```bash
vault write -wrap-ttl=60s -f auth/approle/role/mycourt-backend-role/secret-id
```

This returns a single-use wrapping token, not the secret_id itself. Your deploy script ships that wrapping token to the target VM; Vault Agent unwraps it once on startup to get the real secret_id. If someone intercepts the wrapping token in transit and unwraps it before your agent does, your agent's own unwrap attempt fails — which is a detectable tamper signal (you'd see this in Vault's audit log as a failed unwrap), rather than a silent compromise.

### 4. Scope the policy to the bare minimum

hcl

```hcl
# mycourt-db-policy.hcl
path "database/creds/mycourt-backend-role" {
  capabilities = ["read"]
}
```

That's it — nothing else. This token should not be able to read other secrets engines, other apps' credentials, or manage Vault config. Least privilege means a compromised token for this app can only ever mint MongoDB creds scoped to `mycourt` — not touch Passbolt, n8n's Vault path, or anything else on `vault.mojtel.ir`.

### 5. Turn on audit logging

bash

```bash
vault audit enable file file_path=/vault/logs/audit.log
```

Every login and every credential fetch gets logged with source IP and role name. This is your detection layer — if `mycourt-backend-role` suddenly authenticates from an IP outside your CIDR bind (which would already be blocked, but worth verifying) or authenticates far more often than your deploy cadence, that's a signal.

### 6. If you ever move this to Kubernetes: skip AppRole entirely

You already run a VM-based Kubernetes cluster. If this backend ever runs there, Vault's **Kubernetes auth method** is strictly better than AppRole for this exact problem: instead of a static secret_id you distribute and protect, Vault verifies the pod's own Kubernetes service account token (which Kubernetes already manages, rotates, and scopes for you) directly against the Kubernetes API. There's no secret_id to leak, wrap, or rotate at all — the "credential" is the pod's identity, which only exists as long as the pod does.

**The practical bottom line for your Compose setup today:** short TTL + single-use + CIDR binding + wrapped delivery + a policy scoped to exactly one path. Any one of these alone helps; together, a leaked `role_id`/`secret_id` pair is very likely already expired, already used, or coming from the wrong network by the time anyone could act on it.