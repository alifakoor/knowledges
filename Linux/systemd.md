Systemd is a system and service manager for Linux operating systems.
runs as first process (as PID 1)
it brings up and maintains the user-space services.

it's new version for initd

global configuration: `/lib/systemd/system` or `/usr/lib/systemd/system`
local definitions: `/etc/systemd/system`


### units and unit types:

In systemd, a "[[unit]]" is a resource or service that systemd manages. Think of a unit as a task or a job that the system needs to handle. Each unit has a specific type, defining what kind of task it is. Here are the main types of units, explained simply:

1. **[[Service Unit]] (`.service`)**:
   - Runs a program or service, like a web server or database.
   - Example: `nginx.service` runs the Nginx web server.

2. **[[Socket Unit]] (`.socket`)**:
   - Manages network connections for services.
   - Example: `sshd.socket` listens for SSH connections.

3. **[[Target Unit]] (`.target`)**:
   - Groups other units together.
   - Example: `multi-user.target` starts all the services needed for multi-user mode.

4. **[[Device Unit]] (`.device`)**:
   - Represents a piece of hardware.
   - Example: `dev-sda1.device` for a specific disk drive.

5. **[[Mount Unit]] (`.mount`)**:
   - Manages mounting file systems.
   - Example: `home.mount` mounts the `/home` directory.

6. **[[Automount Unit]] (`.automount`)**:
   - Automatically mounts a file system when it's accessed.
   - Example: `home.automount` automounts `/home`.

7. **[[Swap Unit]] (`.swap`)**:
   - Manages swap space (extra memory on disk).
   - Example: `swap.swap` for a swap file or partition.

8. **[[Path Unit]] (`.path`)**:
   - Monitors a file or directory for changes.
   - Example: `var-log.path` watches the `/var/log` directory.

9. **[[Timer Unit]] (`.timer`)**:
   - Schedules tasks to run at specific times or intervals.
   - Example: `backup.timer` runs a backup service every night.

10. **[[Snapshot Unit]] (`.snapshot`)**:
    - Saves the current state of the system.
    - Example: `maintenance-mode.snapshot` saves the current state for maintenance.

11. **[[Slice Unit]] (`.slice`)**:
    - Groups and limits system resources for processes.
    - Example: `user.slice` limits resources for user processes.

12. **[[Scope Unit]] (`.scope`)**:
    - Manages a group of processes started outside systemd.
    - Example: `session-1.scope` manages all processes of a user session.

Each unit type does a specific job to help manage the system's resources and services efficiently. Units are configured using unit files, which are like instructions telling systemd how to handle each task.


### ***command line for systemd is `systemctl`***

some commands:

`systemctl start/stop/restart/status/reload [app]`

**make the app auto start after reboot:**
`systemctl disable/enable [app]`

`systemctl is-enabled/is-active/is-failed [app]`

**show list of units with their file and status:**
`systemctl list-units`
`systemctl list-unit-files`

**show the list of dependencies of the app:**
`systemctl list-dependencies [app]`

**put the output of the app in `/dev/null`:**
`systemctl mask [app]`
`systemctl unmask [app]`

**editing the app config:**
`systemctl edit [app]`

**reload the daemon:**
`systemctl daemon-reload`
if you change a systemd file, you must reload the daemon



### ***journald is systemd's logging service***

#### ***command line for journald is `journalctl

some commands: 

When used alone, every journal entry that is in the system will be displayed within a pager (usually `less`) for you to browse. The oldest entries will be up top:
`journalctl`

When saving previous boots is enabled on your server, `journalctl` provides some commands to help you work with boots as a unit of division. To see the boots that `journald` knows about, use the `--list-boots` option with `journalctl`:
``` bash
journalctl --list-boots
```


show logs for a special app:
``` bash
journalctl -u [app]
```

show logs for special app and follow:
``` bash
journalctl -u [app] -f
```

show logs based on search regex:
``` bash
journalctl -g [regex_pattern]
```

show logs since 2 days ago:
``` bash
journalctl --since "2 days ago"
journalctl --since yesterday
```

show logs since `date1` until `date2`:
``` bash
journalctl --since [date1] --until [date2]
journalctl --since "2024-01-01" --until "2024-01-30 06:00:00"
journalctl --since "09:00" --until "1 hour ago"
```

show logs that are filtered based on User ID (UID) or Porcess ID (PID):
``` bash
journalctl _UID=108
journalctl _PID=667
```

show volume usage by logs;
``` bash
journalctl --disk-usage
```

 Reduce disk usage below specified size:
``` bash
 journalctl --vacuum-size=BYTES
```
 
 Leave only the specified number of journal files:
``` bash
 journalctl --vacuum-files=INT
```
 
 Remove journal files older than specified time:
``` bash
 journalctl --vacuum-time=TIME
```

