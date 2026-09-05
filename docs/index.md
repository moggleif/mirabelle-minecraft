# Minecraft Server with Crafty Controller

A small, understandable setup for running Minecraft servers through Crafty Controller in Docker.

## Choose what you want to do

### Run Minecraft servers

Start here if you mainly use Crafty to create and manage Minecraft servers.

- [Crafty guide](getting-started/crafty.md) — create servers, manage players, whitelist users, worlds and everyday server administration.
- [Server sizing and ports](guides/server-sizing.md) — memory limits, multiple servers and port allocation.

### Administer the host

Use these guides for Docker, networking, upgrades and recovery.

- [Deployment and operations](operations/deployment.md) — Docker Compose, `.env`, networking, reverse proxy and Crafty upgrades.
- [Backup and recovery](operations/backup-recovery.md) — world backups, off-host protection and rebuilding a host.

### Understand the project

- [Public repository safety](project/public-repo-safety.md) — secret hygiene, Git history and safe public repository practices.
- [Security policy](../SECURITY.md) — how security issues and accidentally committed secrets are handled.

## Architecture

```text
Git                -> deployment definition and documentation
Docker Compose     -> runs Crafty
Crafty Controller  -> manages Minecraft servers and worlds
Persistent storage -> worlds, backups, logs and Crafty state
```

Minecraft administration belongs in Crafty. Linux, Docker, networking and backups remain separate infrastructure concerns.

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

Then follow [Deployment and operations](operations/deployment.md).
