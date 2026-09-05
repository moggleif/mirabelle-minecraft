# Step 3 — Your first server

Everything on this page happens in the Crafty website. No terminal.

Your first server is not precious. Make one, poke at it, break it, delete it. Making a second one takes two minutes. Save your good ideas for the world you build *after* you know how this works.

## What Crafty asks you

When you create a server, Crafty asks a handful of questions. Here is what they mean and what to answer the first time.

| Question | First-time answer | Why |
| --- | --- | --- |
| Server type | **Paper** | Paper is a well-known Minecraft server flavour. It behaves like vanilla Minecraft, runs smoothly, and can take plugins later if you want them. |
| Minecraft version | The version you play | The server and your game must match, or you cannot join. Check your Minecraft launcher first. |
| Name | Something short, like `test` | It is only a label inside Crafty. You can rename it later. |
| Port | `25565` | This is the "door number" players connect to. The first server gets the standard one. |
| Minimum memory | `1 GB` | How much memory the server takes right away. |
| Maximum memory | `3 GB` | The most it is ever allowed to use. |

More about memory and ports on [Memory, ports and extra servers](../guides/server-sizing.md).

Somewhere in the process you will have to accept Minecraft's **EULA** — the licence agreement from Mojang. Every Minecraft server has to. You cannot start a server without it.

## Start it and watch the console

Press start, then open the server's **console** in Crafty. This is the server talking to you in real time, and it is the single most useful screen in Crafty.

The first start is slow. The server is generating a world out of nothing. Wait until a line appears saying it is done and telling you how long it took, something like `Done (34.5s)!`.

If the console fills with red text and stops, do not panic — go to [When something breaks](../guides/troubleshooting.md).

## Join your own server

In Minecraft: Java Edition, go to **Multiplayer** → **Add Server**.

- Playing on the host itself: `localhost`
- Playing on another computer at home: the host's address, for example `192.0.2.10`

If your server uses a port other than `25565`, put it after a colon: `192.0.2.10:25566`.

You should now be standing in your own world. That is the whole thing working.

## Change how the world plays

Game settings live in a file called `server.properties`. Crafty has a settings screen and a file manager for it — you do not need a terminal.

The ones worth knowing early:

| Setting | Does what |
| --- | --- |
| `motd` | The line of text players see in their server list |
| `difficulty` | `peaceful`, `easy`, `normal` or `hard` |
| `gamemode` | `survival`, `creative`, `adventure` or `spectator` |
| `pvp` | Whether players can hurt each other |
| `max-players` | How many people can be online at once |
| `view-distance` | How far players can see. Lowering this is the easiest fix for a laggy server. |

Most changes only take effect after a restart. Use Crafty's restart button rather than stopping and starting by hand.

## Stop, start, restart

Use Crafty's buttons. Do not just close the console or switch the computer off — a Minecraft server keeps parts of the world in memory and writes them out when it shuts down properly. Cutting the power mid-write is how worlds get corrupted.

- **Stop** before you change files or do maintenance.
- **Restart** after settings changes.
- **Start** when it is stopped.

## Making a second world

You have two options, and both are fine:

- **A new world inside the same server** — same version, same settings, fresh terrain.
- **A brand new server** — better when you want a different Minecraft version, a different server type, or a mod pack. Old servers can just sit there, stopped, costing you nothing but disk space.

---

**Next:** [Invite your friends](invite-friends.md)
