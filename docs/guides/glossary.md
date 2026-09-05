# Word list

Every word on this site that might mean nothing to you yet, in plain language. Skim it once; come back when something looks unfamiliar.

## The computer

| Word | What it means |
| --- | --- |
| **Host** | The computer that runs everything and stays switched on. |
| **Terminal** | A window where you type commands instead of clicking. |
| **Command** | One line you type and run, like `docker compose ps`. |
| **`sudo`** | "Do this as the computer's administrator." Asks for your password and shows nothing while you type it. |
| **Linux** | The operating system this guide assumes on the host. |
| **Disk full** | The host has run out of storage. Worlds, backups and logs all grow over time. |

## Docker

| Word | What it means |
| --- | --- |
| **Docker** | Software that runs programs inside sealed boxes, so they cannot make a mess of the computer. |
| **Container** | One running box. Start it, stop it, throw it away, make a new one. |
| **Image** | The template a container is made from. Crafty is distributed as an image. |
| **Docker Compose** | The tool that reads a recipe file and starts containers for you. |
| **`compose.yaml`** | This project's recipe: which image to run, which ports to open, which folders to use. |
| **`.env`** | Your personal settings file, sitting next to the recipe. Never shared, never uploaded. |
| **Bind mount** | A folder on the host that appears inside the container, so data survives when the container is replaced. |
| **Pinned version** | Naming an exact version in the recipe instead of "latest", so upgrades happen when *you* decide. |

## Crafty and Minecraft

| Word | What it means |
| --- | --- |
| **Crafty Controller** | The website that manages your Minecraft servers. Not part of this project — [it has its own docs](https://docs.craftycontrol.com/). |
| **Minecraft server** | One world with its own settings, players and address. You can have several. |
| **Vanilla** | Plain Minecraft, exactly as Mojang ships it. |
| **Paper** | A popular server flavour. Plays like vanilla, runs faster, supports plugins. |
| **Plugin** | An add-on for the server. Players do not install anything. |
| **Mod** | A change to the game itself. Usually every player must install it too. |
| **EULA** | Mojang's licence agreement. Every server has to accept it before it will start. |
| **Console** | The live text feed from a running server. Where errors show up first. |
| **`server.properties`** | The settings file for one Minecraft server. |
| **MOTD** | The line of text players see next to your server in their list. |
| **View distance** | How far players can see. The first thing to lower when the server lags. |

## Players and permissions

| Word | What it means |
| --- | --- |
| **Whitelist** | The guest list. Only these usernames may join. |
| **Operator (op)** | A player with cheat-level commands. Hand out sparingly. |
| **Kick** | Throw someone out. They can come back. |
| **Ban** | Throw someone out and keep them out. |
| **`online-mode`** | The check that a player really is who their username says. Leave it on. |

## Network

| Word | What it means |
| --- | --- |
| **IP address** | A computer's number on a network, like `192.0.2.10`. |
| **`localhost`** | "This computer, the one I am sitting at." Never works from somewhere else. |
| **Port** | A numbered door on a computer. Minecraft's usual door is `25565`; Crafty's is `8443`. |
| **Port forwarding** | Telling the router to send visitors from the internet to a specific computer and port. |
| **Firewall** | The thing that decides which doors are open, and to whom. |
| **LAN** | Your home network. |
| **VPN** | A private tunnel into your home network from outside. Safer than opening ports. |
| **DNS** | The system that turns a name like `example.net` into an address. |
| **SRV record** | A DNS entry that hides a port number behind a name. |
| **HTTPS** | An encrypted web connection. Crafty only uses HTTPS. |
| **Certificate** | The document a site shows to prove who it is. |
| **Self-signed certificate** | One the server made for itself. Works fine; browsers warn about it anyway. |
| **Reverse proxy** | A server that sits in front of Crafty to give it a proper name and a trusted certificate. |

## Backups and code

| Word | What it means |
| --- | --- |
| **Backup** | A copy of your world you can go back to. |
| **Restore** | Putting a backup back. |
| **Off-host backup** | A copy stored somewhere other than the host, so it survives the host dying. |
| **Git** | A tool that tracks every change to a set of files. |
| **Repository (repo)** | A project tracked by Git. This one lives on GitHub. |
| **Clone** | Downloading a repository onto your computer. |
| **Commit** | One saved change, with a note about what you did. |
| **`.gitignore`** | The list of files Git should never pick up — like `.env`. |
| **Secret** | A password, key or token. Never put one in Git, not even briefly. |

---

**Back to:** [Start here](../index.md)
