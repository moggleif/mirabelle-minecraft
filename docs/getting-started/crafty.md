# Crafty user guide

Use Crafty Controller for day-to-day Minecraft administration. You should not need shell access for normal server management.

## Create a server

In Crafty, choose **Create New Server** and select the server type and version you want.

For a small Paper server, a practical starting point is:

- minimum memory: 1 GB
- maximum memory: 3 GB
- first server port: 25565

Use a different port for every simultaneously running server, for example 25566, 25567 and so on.

See [Server sizing and ports](../guides/server-sizing.md) before allocating large amounts of memory or running several servers at once.

## Whitelist

Whitelist settings are per Minecraft server, not global Crafty defaults.

For a private server, enable:

```properties
white-list=true
enforce-whitelist=true
```

These settings live in that server's `server.properties`. Crafty's file manager can edit the file from the web interface.

Add only the players who should be able to join. A whitelist is enough for normal private-server access control; you do not need to ban every other player.

## Players and operators

Use Crafty's player management and server console for normal administration such as:

- adding allowed players
- operator permissions
- kick/ban actions when needed
- console commands

Keep operator access limited to people who actually need administrative powers inside Minecraft.

## Worlds and files

Crafty can manage server files, worlds and configuration through its web interface.

Before changing important world or server files, create a backup.

## Start, stop and restart

Use Crafty's controls rather than Docker or the Linux shell for Minecraft server lifecycle operations.

A normal user should be able to:

- start a server
- stop it cleanly
- restart it
- inspect its console
- edit server files
- create and restore backups

## Backups

Schedule regular Crafty backups for servers that contain worlds you care about.

Crafty backups protect individual Minecraft server data. They are separate from host-level/off-host backups; see [Backup and recovery](../operations/backup-recovery.md).

## Creating another server

When adding another Java server:

1. Choose the desired server software and version.
2. Give it a unique port from the configured range.
3. Choose conservative memory limits.
4. Enable whitelist if the server is private.
5. Add the intended players.
6. Start the server and verify that it works before changing plugins or advanced settings.
7. Configure backups.

## What belongs in Crafty

Use Crafty for Minecraft concerns:

- server creation and deletion
- server versions and types
- Minecraft configuration
- worlds
- console
- players
- plugins/mods where applicable
- backups and restores

Host-level tasks such as Docker upgrades, firewall rules, reverse proxy, Git deployment and disaster recovery belong to the host administrator. See [Deployment and host operations](../operations/deployment.md).
