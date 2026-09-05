# Backup and recovery

Git, Crafty backups and off-host backups protect different parts of the system. Use all three when the worlds matter.

## What Git protects

Git protects the deployment definition and documentation, such as:

- `compose.yaml`
- `.env.example`
- documentation
- repository workflows and policy files

Git should not contain live Minecraft worlds, Crafty runtime state, passwords, tokens, certificates or private deployment configuration.

## What Crafty backups protect

Crafty backups protect Minecraft server data such as worlds and server files.

Schedule backups for servers that contain data you care about. Test that a backup can be restored before relying on the schedule as your only recovery plan.

## Off-host backup

A backup stored only on the same VM or disk does not protect against loss of that VM or storage device.

Copy important Crafty backups and/or the persistent Crafty data to another system on a regular schedule.

Good destinations include:

- another host
- NAS storage
- dedicated backup storage
- an appropriate cloud backup target

The exact destination is deployment-specific and should not be hard-coded into this public repository.

## Before upgrades

Before changing the Crafty image version or making significant host changes:

1. Confirm recent Minecraft backups exist.
2. Confirm important backups have reached off-host storage.
3. If the virtualization platform supports snapshots, consider taking a short-lived VM snapshot as an additional rollback aid.
4. Perform the change deliberately.
5. Verify Crafty and the Minecraft servers afterward.

A VM snapshot is useful for short-term rollback but is not a substitute for a real backup.

## Recovery: lost Minecraft world

If Crafty and the host are healthy but a world/server needs to be restored:

1. Stop the affected Minecraft server.
2. Select a known-good Crafty backup.
3. Restore it through Crafty.
4. Start the server.
5. Verify the world before resuming normal use.

## Recovery: lost Crafty host

If the VM or host is lost:

1. Provision a replacement Linux host with Docker and Git.
2. Clone this repository.
3. Create a fresh local `.env` from `.env.example`.
4. Recreate the persistent data location.
5. Restore Crafty persistent data/backups from off-host storage.
6. Run `docker compose config`.
7. Pull and start the pinned Crafty image.
8. Verify Crafty.
9. Verify each Minecraft server and its port.
10. Verify backups again after recovery.

The repository makes rebuilding the service predictable, while the separate backup set restores the state that Git intentionally does not contain.

## Recovery priorities

Think of the system in layers:

```text
Git repository       -> how the service is built
Crafty persistent data -> current service/game state
Crafty backups       -> recover individual servers/worlds
Off-host backup      -> survive loss of the host/storage
```

Keeping these layers separate makes failures easier to reason about and prevents the Git repository from becoming a storage location for sensitive or constantly changing runtime data.
