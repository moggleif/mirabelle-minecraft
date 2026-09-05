# Deployment and host operations

This guide covers the host-side setup around Crafty Controller: Docker, persistent storage, networking and deliberate upgrades.

## Prerequisites

Install:

- Linux
- Docker Engine
- Docker Compose plugin
- Git

Clone the repository and create a local environment file:

```bash
git clone <repository-url>
cd <repository-directory>
cp .env.example .env
```

Edit `.env` for the host. Keep `.env` out of Git.

## Persistent data

Crafty runtime data must live outside the Git working tree. The Compose file expects a host path configured with `CRAFTY_DATA_DIR`.

A typical layout is:

```text
crafty-data/
├── backups/
├── config/
├── import/
├── logs/
└── servers/
```

Create the directory structure before starting the stack if needed.

## Validate and start

Always validate the resolved Compose configuration before applying it:

```bash
docker compose config
```

Then pull and start the pinned Crafty image:

```bash
docker compose pull
docker compose up -d
```

Check status and recent logs:

```bash
docker compose ps
docker compose logs --tail=100
```

## Networking

Crafty's HTTPS administration interface should normally remain private to trusted networks, for example LAN or VPN.

Minecraft game ports are separate. Expose only the ports actually needed by players.

The repository uses a small configurable Java port range. Every simultaneously running Minecraft server must use a unique port from that range.

Do not expose the Crafty administration interface publicly unless there is a deliberate security design for doing so.

## Reverse proxy

A reverse proxy may terminate TLS in front of Crafty. Keep that configuration deployment-specific rather than committing private hostnames, addresses or certificates to this repository.

If access to Crafty is intended only for trusted networks, enforce that with reverse-proxy ACLs, firewall policy, VPN access or equivalent controls.

## Upgrades

The Crafty image is intentionally pinned to a specific version in `compose.yaml`.

Upgrade deliberately:

1. Read the release notes.
2. Confirm that recent backups exist.
3. Change the image version in Git.
4. Let repository checks validate the change.
5. Review and merge the pull request.
6. Pull the updated repository on the host.
7. Run `docker compose pull`.
8. Run `docker compose up -d`.
9. Verify Crafty and at least one Minecraft server.

Avoid unattended container upgrades for this setup. A controlled upgrade is easier to troubleshoot and roll back.

## Updating the deployment

After a reviewed Git change is merged:

```bash
git pull --ff-only
docker compose config
docker compose pull
docker compose up -d
```

Then verify:

```bash
docker compose ps
docker compose logs --tail=100
```

## Separation of responsibilities

Crafty users should be able to perform normal Minecraft administration through the Crafty web interface without needing shell access.

Host administrators remain responsible for:

- Linux
- Docker
- networking
- TLS/reverse proxy
- Git deployment changes
- host-level backups
- recovery of the underlying service

This separation keeps routine Minecraft administration simple without giving unnecessary access to the host operating system.
