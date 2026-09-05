# Crafty user guide

This document is for the person who manages Minecraft through the Crafty web interface.

The intended operating model is simple:

- use **Crafty** for Minecraft administration;
- use the Linux host only for infrastructure work;
- create, test, discard and recreate Minecraft servers freely;
- rely on backups for anything worth keeping.

## What Crafty is for

Crafty is the control panel for Minecraft. From the web interface an administrator can:

- create and delete Minecraft servers;
- choose server software and Minecraft version;
- start, stop and restart servers;
- view and use the server console;
- manage files such as `server.properties`;
- manage players, operators and bans;
- create and restore backups;
- run several separate Minecraft servers on the same host.

A Crafty administrator does not normally need SSH access to the Linux host for day-to-day Minecraft work.

## Creating a server

For a normal Java survival server, **Paper** is a good default. It is widely used, compatible with normal Java clients and gives room for plugins later.

A simple first-server checklist:

1. Choose **Paper**.
2. Choose the Minecraft version you want to play.
3. Give the server a clear name.
4. Assign a unique port.
5. Choose sensible minimum and maximum memory values.
6. Create the server.
7. Start it and wait until the console reports that startup has completed.
8. Enable whitelist before inviting players.
9. Add the players who should be allowed to join.
10. Create a backup after the initial setup is working.

See [SERVER-SIZING.md](SERVER-SIZING.md) for memory and port guidance.

## Whitelist

Whitelist is configured **per Minecraft server**. It is not a global Crafty setting.

For a private server, enable both:

```properties
white-list=true
enforce-whitelist=true
```

These values live in that server's `server.properties` file and can be edited from Crafty's file manager.

Players can then be added from Crafty or from the Minecraft console:

```text
whitelist add PlayerName
```

Players who are not on the whitelist are refused automatically. They do not need to be banned.

Use the ban list only when there is a reason to block a specific player.

## Ports

Every Minecraft server that runs at the same time needs its own port.

A common convention is:

```text
First server   25565
Second server  25566
Third server   25567
...
```

The host administrator should define which port range is available. Stay inside that range when creating new servers.

The default Java Minecraft port is `25565`. Clients can connect to that server without typing a port. Other ports normally need to be written explicitly, for example:

```text
minecraft.example.net:25566
```

DNS SRV records can later be used if several servers should have separate names without visible port numbers.

## Memory

For a small Paper server with only a few players, a useful starting point is:

```text
Minimum memory: 1 GB
Maximum memory: 3 GB
```

Do not assume that more memory always makes Minecraft faster. Performance can also depend on CPU speed, chunk generation, view distance, plugins and mods.

If several servers are running simultaneously, their combined memory limits must leave enough memory for Linux, Docker and Crafty itself.

See [SERVER-SIZING.md](SERVER-SIZING.md) for examples.

## Starting, stopping and restarting

Prefer Crafty's controls rather than killing processes manually.

- **Start** when a server is stopped.
- **Stop** before risky file changes or some maintenance tasks.
- **Restart** after configuration changes that require a restart.

If a server crashes, inspect its console and logs in Crafty. A crash is usually a server problem, not a Crafty problem.

## New world vs new server

If a world is no longer wanted, there are two reasonable approaches:

- create a new world inside the existing server; or
- create a completely new server instance.

Creating a new server is often cleaner when experimenting with a different Minecraft version, server type, plugin set or modpack.

Keeping several old servers is fine as long as they are stopped when not needed and disk usage is monitored.

## Backups

Create backups before:

- major Minecraft upgrades;
- changing server software;
- installing large plugin or mod changes;
- experimenting with a world you care about;
- deleting a server.

Backups are not only for disasters. They make experimentation cheap.

See [BACKUP-RECOVERY.md](BACKUP-RECOVERY.md).

## Things that belong outside Crafty

The following are host/infrastructure tasks rather than Minecraft tasks:

- Docker upgrades;
- Crafty container upgrades;
- Linux updates;
- DNS;
- router/firewall/port-forwarding rules;
- reverse proxy and TLS certificates;
- off-host backups;
- Git repository maintenance.

These are covered in the infrastructure documentation rather than this guide.
