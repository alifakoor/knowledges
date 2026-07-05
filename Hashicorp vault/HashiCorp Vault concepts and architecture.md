---
title: HashiCorp Vault concepts and architecture
source: https://claude.ai/chat/e0fb43f5-e365-4fe9-9baf-590296d5f144
author:
published:
created: 2026-07-05
description: Claude conversation with 8 messages
tags:
  - hashicorp
  - vault
---
### Step 1: What problem does Vault solve?

Every system has secrets — database passwords, API keys, TLS certificates, cloud credentials. The naive approach is to hardcode them in config files or env vars. Problems: they leak into git repos, they never rotate, everyone who can read the file can read the secret, and there's no audit trail of who accessed what.

Vault is a **centralized secrets management system**. Instead of secrets living scattered across your infrastructure, they live in one place, behind authentication, authorization, and audit logging. Instead of static secrets, Vault can generate **dynamic, short-lived credentials** on demand.

### Step 2: The core mental model

Vault is fundamentally a **secure, encrypted key-value store with an API in front of it**, plus a pluggable system for authentication and secret generation. Everything happens through this flow:

**Client → authenticates → gets a token → uses token to request a secret → Vault checks policy → returns secret (maybe generated on the fly) → secret has a lease/TTL**

Let me define each of those pieces.

### Step 3: Core concepts

**Secrets Engines** — these are plugins that store, generate, or encrypt data. Examples:

- **KV (Key-Value)** — the simplest one, just stores static secrets (like a password) at a path, e.g. `secret/data/myapp/db`.
- **Database secrets engine** — generates *dynamic* short-lived DB credentials on request, then revokes them after the lease expires. No more shared static DB passwords.
- **PKI engine** — issues TLS certificates on demand, acts as a certificate authority.
- **Transit engine** — "encryption as a service." Your app sends plaintext, gets ciphertext back — Vault never stores the data itself, just does crypto operations.
- Others: AWS/GCP/Azure dynamic credentials, SSH, TOTP, etc.

**Auth Methods** — these are plugins for *proving who you are* to Vault. This is exactly the part you already used with n8n:

- **Token** — the rawest form, a token is directly presented.
- **AppRole** — designed for machines/apps (not humans). You get a `role_id` (like a username, can be baked into config) and a `secret_id` (like a password, usually delivered securely and often single-use). This is the standard way to let an app authenticate itself.
- **Userpass** — simple username/password, mostly for humans/testing.
- Others: LDAP, GitHub, Kubernetes (service account tokens), TLS certs, cloud IAM.

**Policies** — HCL/JSON documents that define what paths a token can do what with (read/write/list/delete). Example:

hcl

```hcl
path "secret/data/myapp/*" {
  capabilities = ["read"]
}
```

Auth methods map an identity to one or more policies. Policies are Vault's authorization layer — authentication (who you are) and authorization (what you can do) are deliberately separate.

**Tokens** — the universal "session" concept. Every authenticated request in Vault is backed by a token internally, even if you logged in via AppRole or LDAP — that auth method just gets you a token. Tokens have:

- **TTL** (time to live) — expire and must be renewed.
- **Attached policies** — inherited permissions.

**Leases** — most secrets returned by Vault come with a lease. When the lease expires, Vault can automatically revoke the secret (e.g., delete the dynamic DB user). This is how Vault limits the blast radius of a leaked credential — it's often already dead by the time someone could misuse it.

**Seal / Unseal** — this is the concept that trips people up most. Vault encrypts all its data at rest with an encryption key. That key is itself encrypted with a "root key," which is split using **Shamir's Secret Sharing** into multiple key shares (default 5, with a threshold of 3 needed). When Vault starts, it's in a **sealed** state — it literally cannot read its own storage. Someone must provide the threshold number of unseal keys to reconstruct the root key and unseal it. In production, this manual step is usually replaced by **auto-unseal** using a cloud KMS (AWS KMS, GCP KMS, Azure Key Vault, or Transit from another Vault) so a human isn't needed every restart.

**Storage Backend** — where the encrypted data physically lives. Historically Consul was the recommended backend; today most deployments use **Integrated Storage (Raft)**, which is built into Vault itself — no external Consul cluster needed. This backend also handles clustering/replication.

### Step 4: Architecture — putting it together

Let me show you the shape of this visually.
![[vault_request_flow.svg|646]]
Every request travels down this chain, and the response (secret + lease) comes back up the same way. Everything below "Vault core" only happens if the token's attached policy allows it.

### Step 5: Deployment architecture (clustering/HA)

In a real deployment you don't run one Vault process:

- **Multiple Vault server nodes** form a cluster. One node is **active** (handles all reads/writes); the others are **standby**, ready to take over if the active node dies.
- With **Integrated Storage (Raft)**, these nodes also replicate the encrypted data among themselves using the Raft consensus protocol — so you typically want an odd number (3 or 5) for quorum, the same logic you already know from etcd on your k8s masters.
- A **load balancer** (or Vault's own request forwarding) sits in front and routes clients to the active node.
- **Enterprise only**: Performance Replication (across regions) and DR Replication (a whole standby cluster) for disaster recovery, plus **Namespaces** (multi-tenant isolation within one cluster).

### Step 6: How this maps to what you've already done

You've already touched a good chunk of this in the n8n/Vault integration: you configured **AppRole** auth (role\_id + secret\_id) so n8n could authenticate as an application rather than a human, tuned **token renewal** so credentials don't silently expire mid-workflow, and dealt with **TLS/DNS** because Vault refuses plaintext by default for anything security-sensitive. That's steps 3 (auth methods) and the token lifecycle piece of the picture above, applied in Docker Compose.

If it'd help, a natural next step would be walking through the KV v2 vs database secrets engine tradeoff for something like Passbolt/MongoDB credential management, or the Raft cluster setup itself since you're already comfortable with quorum concepts from your Kubernetes etcd work — just say which.


-----

**Vault sits beside the connection, not inside it.** Your NestJS app talks to Vault once to get credentials, then talks directly to MongoDB with those credentials. Vault never proxies your queries.

![[vault_nestjs_mongo_placement.svg|697]]

**Vault is not a proxy or a gateway.** It's a credential factory that sits off to the side. Your NestJS process is the only thing that ever opens a socket to MongoDB.