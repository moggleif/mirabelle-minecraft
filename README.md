# Minecraft Server with Crafty Controller

A reusable single-host setup for running Minecraft servers through **Crafty Controller** in Docker.

The design goal is to keep the system understandable and recoverable:

```text
Git                -> deployment definition and documentation
Docker Compose     -> runs Crafty
Crafty Controller  -> manages Minecraft servers and worlds
Persistent storage -> worlds, backups, logs and Crafty state
```

Minecraft administration happens in Crafty. Linux, Docker, networking and backups remain separate infrastructure concerns.

## Documentation

The documentation is published with GitHub Pages from `/docs`:

**[Open the documentation site](https://moggleif.github.io/mirabelle-minecraft/)**

Or jump directly to the guide that matches what you are doing:

| Guide | Use it for |
| --- | --- |
| [Crafty user guide](docs/getting-started/crafty.md) | Creating servers, whitelist, players, worlds and everyday Minecraft administration |
| [Server sizing and ports](docs/guides/server-sizing.md) | Memory limits, multiple servers and port allocation |
| [Deployment and host operations](docs/operations/deployment.md) | Docker, `.env`, networking, reverse proxy and Crafty upgrades |
| [Backup and recovery](docs/operations/backup-recovery.md) | World backups, off-host protection and rebuilding a host |
| [Public repository safety](docs/project/public-repo-safety.md) | Secret hygiene, privacy, Git history and checks before publishing the repository |
| [Security policy](SECURITY.md) | Reporting security problems and handling accidentally committed secrets |

## Why Crafty?

Crafty gives Minecraft users a web interface where they can create and remove servers, choose versions, start and stop them, use the console, edit files and manage backups without requiring shell access to the host.

That makes it a useful middle layer:

```text
Minecraft user
      ↓
Crafty web UI
      ↓
Minecraft server instances

Host administrator
      ↓
Git / Docker / Linux / network / backup
```

The two roles may of course be held by the same person.

## Repository contents

```text
.
├── compose.yaml
├── .env.example
├── .gitignore
├── README.md
├── SECURITY.md
├── .github/
│   ├── dependabot.yml
│   ├── pull_request_template.md
│   ├── rulesets/
│   └── workflows/
└── docs/
    ├── index.md
    ├── _config.yml
    ├── getting-started/
    │   └── crafty.md
    ├── guides/
    │   └── server-sizing.md
    ├── operations/
    │   ├── deployment.md
    │   └── backup-recovery.md
    └── project/
        └── public-repo-safety.md
```

The repository intentionally does **not** contain Minecraft worlds or Crafty runtime data.

## Runtime data

Persistent data should live outside the Git working tree, for example:

```text
crafty-data/
├── backups/
├── config/
├── import/
├── logs/
└── servers/
```

The paths are deployment-specific and configured through `.env`/Compose bind mounts.

Do not commit runtime data, passwords, tokens, private keys or certificates.

## Quick start

Prerequisites:

- Linux
- Docker Engine
- Docker Compose plugin
- Git

Clone the repository and create the local environment file:

```bash
git clone <repository-url>
cd <repository-directory>
cp .env.example .env
```

Edit `.env`, create the persistent Crafty directories, then validate and start the deployment:

```bash
docker compose config
docker compose pull
docker compose up -d
```

Check it with:

```bash
docker compose ps
docker compose logs --tail=100
```

Detailed deployment instructions are in [Deployment and host operations](docs/operations/deployment.md).

## Design principles

### Infrastructure in Git, game data outside Git

Git should describe how the service is built, not contain the constantly changing Minecraft worlds.

### Pin the Crafty version

Use a specific Crafty image version rather than an automatically moving tag. Upgrades then become deliberate, reviewable Git changes.

### Keep the administrative UI private

The Crafty web interface normally only needs trusted LAN/VPN access. Minecraft game ports can be exposed separately to players.

### Give each Minecraft server a unique port

Several server instances can coexist in Crafty. Each running server needs its own port. A small configurable port range makes it possible to create new servers without publishing an unnecessarily large network surface.

### Back up data independently

Git protects the deployment definition. Crafty backups protect individual worlds and servers. Off-host backups protect against loss of the VM, disk or host.

### Treat a public repository as public history

Removing a secret from the current branch does not remove it from old commits. This repository runs a full-history Gitleaks scan on pushes and pull requests, and [Public repository safety](docs/project/public-repo-safety.md) contains a checklist for public repository changes.

## Scope

This repository is aimed at home servers, family/friends servers, labs and other small single-host Minecraft installations.

It deliberately avoids the complexity of clustered game-hosting platforms. The objective is a system that is easy to understand, easy to operate through Crafty and straightforward to rebuild when something breaks.
