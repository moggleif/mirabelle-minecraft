# Deployment and host operations

This document is for the person responsible for the Linux host, Docker, networking and Crafty itself.

Minecraft administration should normally happen in Crafty instead. See [Crafty user guide](../getting-started/crafty.md).

## Repository vs runtime data

Keep the Git repository and Crafty runtime data separate.

Repository:

```text
.
├── compose.yaml
├── .env.example
├── .gitignore
├── README.md
└── docs/
```

Runtime data:

```text
crafty-data/
├── backups/
├── config/
├── import/
├── logs/
└── servers/
```

Do not commit runtime data to Git.

## Initial deployment

Clone the repository:

```bash
git clone <repository-url>
cd <repository-directory>
```

Create the local environment file:

```bash
cp .env.example .env
```

Edit `.env` for the host. It is intentionally excluded from Git.

Create the persistent runtime directories at the path selected in `.env`.

Then validate Compose:

```bash
docker compose config
```

Pull and start Crafty:

```bash
docker compose pull
docker compose up -d
```

Inspect status and logs:

```bash
docker compose ps
docker compose logs --tail=100
```

## Version pinning

The Compose file should use a specific Crafty release rather than an automatically moving tag.

Example:

```yaml
image: registry.gitlab.com/crafty-controller/crafty-4:4.x.y
```

This keeps deployments reproducible and makes upgrades visible in Git history.

## Upgrading Crafty

A deliberate upgrade flow is preferred:

1. Read the release notes.
2. Verify that important Minecraft data is backed up.
3. Optionally take a VM or host snapshot.
4. Change the Crafty image version in `compose.yaml`.
5. Run `docker compose pull`.
6. Run `docker compose up -d`.
7. Verify Crafty login, server list and one Minecraft server.
8. Commit the version change to Git.

Avoid unattended container upgrades for this type of stateful service.

## Networking model

Treat the Crafty web interface and Minecraft game traffic as separate services.

A sensible pattern is:

```text
Crafty web UI
    -> private LAN/VPN access
    -> optional reverse proxy with HTTPS

Minecraft game ports
    -> selectively exposed to the Internet
    -> forwarded directly to the Minecraft host
```

The Crafty administrative interface does not need to be publicly reachable just because players need public Minecraft access.

## Minecraft Java port range

`compose.yaml` publishes a small configurable Java port range. The default is defined in `.env.example`:

```text
MC_JAVA_PORT_RANGE=25565-25575
```

Each simultaneously running Crafty server gets one unique port inside that range.

If users should be able to create several public Minecraft servers without requiring a router change every time, forward the same small range 1:1 to the host, for example:

```text
WAN TCP 25565-25575
        ->
host TCP 25565-25575
```

Choose a range appropriate to the installation. Do not expose a much larger range merely for convenience.

Minecraft Bedrock is **not** published by the default Compose configuration. If Bedrock is actually required, add its UDP port deliberately and document the change rather than exposing unused services by default.

## Crafty HTTPS port

Crafty's HTTPS host port is configurable through:

```text
CRAFTY_HTTPS_PORT=8443
```

Publishing a Docker port makes it reachable on host interfaces unless additional network controls restrict it. Protect Crafty's administrative interface with the host firewall, LAN/VPN policy, reverse-proxy ACLs, or equivalent controls.

## Reverse proxy

A reverse proxy can provide a normal HTTPS hostname for Crafty while the container continues to listen on its internal HTTPS port.

The proxy should forward WebSocket traffic correctly where required and use a trusted TLS certificate.

For a private administration service, access restrictions should normally be enforced at the proxy, firewall or VPN layer.

## Host maintenance

Routine host maintenance includes:

- Linux security updates;
- Docker Engine updates;
- monitoring free disk space;
- verifying backups;
- checking container health after restarts;
- reviewing Crafty releases before upgrades.

Minecraft worlds and server settings remain Crafty-level concerns unless recovery is required.

## Useful commands

Status:

```bash
docker compose ps
```

Recent logs:

```bash
docker compose logs --tail=100
```

Follow logs:

```bash
docker compose logs -f
```

Restart Crafty container:

```bash
docker compose restart
```

Stop the deployment:

```bash
docker compose down
```

Start it again:

```bash
docker compose up -d
```

Removing the container does not remove bind-mounted Crafty runtime data, but backups should still exist before destructive maintenance.
