# Step 1 — How it works

Before you type a single command, it helps to know what you are actually building. There are four pieces, stacked on top of each other.

```text
The computer      the machine that stays switched on
   Docker         keeps installed software in tidy boxes
   Crafty         the website where you press the buttons
   Your servers   the actual Minecraft worlds people join
```

## The computer

Somewhere there is a real computer that stays on. In this guide it is called the **host**. When your friends are playing, this machine is doing the work.

If you turn it off, the server goes away. That is the whole trick: a Minecraft server is just a program running on a computer that never sleeps.

## Docker

Installing server software the normal way makes a mess. Files end up all over the computer, versions clash, and removing things later is painful.

**Docker** solves that. It runs software inside a *container*: a sealed box with everything the program needs inside it. You can start the box, stop it, throw it away and get a fresh one, and the rest of the computer never notices.

You will only use a handful of Docker commands, and this guide gives you all of them.

> **Compose file, in one sentence:** `compose.yaml` in this project is a recipe that tells Docker exactly which box to run and how — so you never have to remember a long command.

## Crafty Controller

**Crafty** is a control panel for Minecraft servers. It is a website that runs on your host, and you open it in a normal browser.

Instead of typing commands to create a server, edit config files by hand and read log files in a terminal, you click buttons. Crafty can:

- create and delete Minecraft servers
- pick which Minecraft version each one runs
- start, stop and restart them
- show you the server console
- manage players, admins and bans
- make and restore backups

Crafty is not made by this project. It has [its own documentation](https://docs.craftycontrol.com/), which is the right place to look for details about its features.

## Your Minecraft servers

Each server Crafty creates is a separate world with its own settings, its own players and its own address. You can have several. They only compete for the computer's memory when they are running at the same time.

## Who does what

This split matters, because it tells you which page to open when you have a question.

| Job | Where you do it |
| --- | --- |
| Make a new world, change game rules, add players, restore a backup | In Crafty, in your browser |
| Start or update Crafty itself, open ports on the router, update Linux | In a terminal on the host |

Most days you will only touch Crafty. The terminal is for setup and maintenance.

> **Rule of thumb:** if it is about Minecraft, it is in Crafty. If it is about the computer, it is in the terminal.

## Where your stuff is kept

Two kinds of files, kept deliberately apart:

- **The recipe** — `compose.yaml`, the docs you are reading, settings examples. This lives in Git, and it is what you would copy to a new computer.
- **The real data** — your worlds, player data, backups, logs, Crafty's own settings. This lives in a folder on the host, outside the project folder, and it is never uploaded to GitHub.

That is why a backup of the project is *not* a backup of your world. See [Keep it safe](../operations/backup-recovery.md).

<div class="pager" markdown="1">

- [← Start here](../index.md)
- [Next: Step 2 — Set up Crafty →](start-crafty.md)

</div>
