# Backup and recovery

This setup deliberately separates infrastructure configuration from Minecraft runtime data. They need different backup strategies.

## What Git protects

Git protects the reproducible parts of the deployment:

- `compose.yaml`;
- documentation;
- helper scripts;
- example configuration;
- upgrade history.

Git is **not** the backup system for Minecraft worlds.

## What must be backed up separately

Crafty runtime data includes:

- Minecraft worlds;
- server configuration;
- Crafty state;
- plugins and mods;
- backups created from Crafty;
- other files stored under the persistent Crafty data directory.

This data should be copied to storage outside the VM or host.

## Three useful layers

A practical model is:

```text
Git remote
    -> infrastructure configuration

Crafty backups
    -> convenient world/server rollback

Off-host backup
    -> protection from VM, disk or host loss
```

Each layer solves a different problem.

## When to create a Crafty backup

Back up before:

- upgrading Minecraft versions;
- changing server software;
- large plugin or mod changes;
- experimental configuration changes;
- deleting a server or world;
- any change where losing progress would be annoying.

For worlds that matter, scheduled backups are preferable to relying on memory.

## Consistency

Minecraft writes world data while it is running. A backup method should therefore either coordinate correctly with the server or stop/quiesce the server while files are copied.

Do not assume that copying a live world directory with arbitrary filesystem tools always produces a clean recovery point.

Use Crafty's backup facilities for normal server-level backups, and test restores occasionally.

## Off-host backup

Crafty's local backup directory should itself be copied somewhere independent of the Minecraft host.

Examples include:

- another NAS or storage system;
- a separate backup server;
- encrypted cloud/object storage;
- another physical disk managed by a proper backup system.

A backup that exists only on the same VM or same physical storage does not protect against loss of that storage.

## Recovery of one Minecraft server

For an ordinary server-level problem:

1. Stop the affected server if necessary.
2. Choose a known-good Crafty backup.
3. Restore it using Crafty's restore workflow.
4. Start the server.
5. Check the console for errors.
6. Join the server and verify the world.

## Recovery of the whole host

On a replacement Linux host:

1. Install Docker and Git.
2. Clone this repository.
3. Create `.env` from `.env.example` and adapt local paths.
4. Restore the persistent Crafty data from off-host backup.
5. Verify permissions and bind-mount paths.
6. Run `docker compose config`.
7. Run `docker compose up -d`.
8. Verify Crafty, its server list and the Minecraft servers.
9. Restore DNS/firewall/reverse-proxy configuration as needed.

The repository recreates the **deployment definition**. The runtime backup recreates the **actual Minecraft state**.

## Test restores

A backup is only useful if it can be restored.

Occasionally test a restore to a disposable Minecraft server or temporary environment. This verifies both the backup files and the recovery process without risking the active world.
