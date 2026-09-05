# Your own Minecraft server

This site walks you through building a Minecraft server that you run and look after yourself.

You do not need to be an expert. You need a computer that can stay switched on, a bit of time, and a willingness to type things that look scary at first. Every step explains what you are doing and why.

> **Is Crafty already installed on your computer?** Then the hard part is done. Skip straight to [Step 3 — Your first server](getting-started/first-server.md), and read [Opening Crafty](getting-started/start-crafty.md#opening-crafty-when-someone-else-set-it-up) if you have not logged in before.

## The steps

<div class="cards" markdown="1">

- [**Step 1 — How it works**](getting-started/how-it-works.md) The four pieces of the puzzle, explained without jargon.
- [**Step 2 — Set up Crafty**](getting-started/start-crafty.md) Get the control panel running and log in for the first time. Skip if it is already installed.
- [**Step 3 — Your first server**](getting-started/first-server.md) Create a world, start it, and join it yourself.
- [**Step 4 — Invite your friends**](getting-started/invite-friends.md) Whitelists, addresses, and who is allowed to do what.
- [**Step 5 — Keep it safe**](operations/backup-recovery.md) Backups, so a bad day never costs you your world.

</div>

And whenever you need them:

<div class="cards" markdown="1">

- [**When something breaks**](guides/troubleshooting.md) The usual problems, and how to fix them yourself.
- [**Word list**](guides/glossary.md) Every confusing word on this site, in plain language.

</div>

## What you need

**If Crafty is already running** — someone set it up for you, or you finished Step 2 — you only need:

- The address of the computer Crafty runs on, and a Crafty login. Ask whoever set it up.
- Minecraft: Java Edition on the computer you play on.

That is genuinely all. Everything below is only for setting up a new machine.

**If you are starting from nothing**, you also need:

- A computer running Linux that can stay on while people play. An old laptop or a small home server is fine.
- Permission to install things on it. Ask whoever owns the computer.
- [Docker Engine and the Docker Compose plugin](https://docs.docker.com/engine/install/) installed on it.
- Git installed, so you can copy this project onto it.

> **No Linux?** This guide assumes Linux. The Crafty parts still make sense on other systems, but the terminal commands will not match.

## Other pages

| Page | What it is for |
| --- | --- |
| [Memory, ports and extra servers](guides/server-sizing.md) | How much memory a server needs, and how to run more than one |
| [Host and Docker notes](operations/deployment.md) | The maintenance jobs: upgrades, networking, restarts |
| [Public repository safety](project/public-repo-safety.md) | What to check before sharing this project's code publicly |
| [Security policy](https://github.com/moggleif/mirabelle-minecraft/blob/main/SECURITY.md) | How to report a security problem |

<div class="pager" markdown="1">

- [Start with Step 1 — How it works →](getting-started/how-it-works.md)

</div>
