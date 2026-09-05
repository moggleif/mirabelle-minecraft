# Host and Docker notes

This page is the reference for looking after the machine, rather than the Minecraft servers on it. Setting Crafty up for the first time is [Step 2](../getting-started/start-crafty.md); this is everything that comes after.

Day to day you should not need this page. Reach for it when you are upgrading, changing the network, or something on the host needs attention.

## Two kinds of files, kept apart

The project folder holds the recipe:

```text
.
├── compose.yaml
├── .env.example
├── .gitignore
├── README.md
└── docs/
```

The data folder holds everything real:

```text
crafty-data/
├── backups/
├── config/
├── import/
├── logs/
└── servers/
```

The data folder lives outside the project folder and never goes into Git. That separation is the reason you can rebuild this setup on a new machine in ten minutes.

## Commands worth knowing

Run all of these from inside the project folder.

| Command | What it does |
| --- | --- |
| `docker compose ps` | Is Crafty running? |
| `docker compose logs --tail=100` | The last 100 lines of Crafty's output |
| `docker compose logs -f` | Follow the output live (`Ctrl+C` to stop watching) |
| `docker compose restart` | Restart Crafty |
| `docker compose up -d` | Start it |
| `docker compose down` | Stop and remove the container |
| `docker compose config` | Check the recipe without changing anything |
| `df -h` | How much disk space is left |

`docker compose down` sounds alarming and is not. It removes the container, not your data — worlds and backups live in the data folder on the host. Even so, do not do it while people are playing.

## Pin the Crafty version

`compose.yaml` names an exact Crafty release rather than a tag that quietly moves:

```yaml
image: registry.gitlab.com/crafty-controller/crafty-4:4.x.y
```

That way upgrades happen when you decide, they show up as a visible change in Git, and if a new version misbehaves you know exactly what changed.

## Upgrading Crafty

Do it deliberately, not automatically:

1. Read Crafty's release notes.
2. Check that your Minecraft data is backed up.
3. Take a snapshot of the machine if you can.
4. Change the version in `compose.yaml`.
5. `docker compose pull`
6. `docker compose up -d`
7. Log in, check the server list, start one server.
8. Commit the version change to Git.

Avoid tools that update this container on their own. It holds state you care about.

## Networking

Treat the Crafty web interface and Minecraft game traffic as two completely different things:

```text
Crafty web UI
    -> home network or VPN only
    -> optionally behind a reverse proxy with HTTPS

Minecraft game ports
    -> may be opened to the internet on purpose
    -> forwarded to the host
```

Players needing to reach Minecraft is not a reason to expose Crafty. Crafty can delete every world you have; the game port cannot.

### The Minecraft port range

`compose.yaml` publishes the range set in `.env`:

```text
MC_JAVA_PORT_RANGE=25565-25575
```

If servers should be reachable from the internet, forward that same range to the host, one-to-one:

```text
WAN TCP 25565-25575
        ->
host TCP 25565-25575
```

Keep the range small. Do not forward a wide range for convenience — you would be opening doors to rooms you have not built yet.

Minecraft Bedrock is **not** published by default. If you genuinely need it, add its UDP port on purpose and write down that you did.

### Crafty's web port

Set through `.env`:

```text
CRAFTY_HTTPS_PORT=8443
```

Publishing a port in Docker makes it reachable on the host's network interfaces unless something else stops it. Restricting it is your job: host firewall, LAN or VPN policy, or a reverse proxy with access rules.

### Reverse proxy

A reverse proxy gives Crafty a proper hostname and a trusted certificate, so the browser stops warning you. It must forward WebSocket traffic for Crafty's live console to work.

A reverse proxy is a convenience, not a protection. Keep the firewall or VPN rules regardless.

## Routine maintenance

- Linux security updates
- Docker Engine updates
- Watch free disk space — worlds, backups and logs only grow
- Check that backups are actually happening, and restore one occasionally
- Check containers came back healthy after a reboot
- Read Crafty's release notes before upgrading

---

**See also:** [Keep it safe](backup-recovery.md) for the backup and rebuild procedures.
