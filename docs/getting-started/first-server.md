# Step 3 — Your first server

Everything on this page happens in the Crafty website, in your browser. Nothing here needs the computer's terminal.

Your first server is not precious. Make one, poke at it, break it, delete it. Making a second one takes two minutes. Save your good ideas for the world you build *after* you know how this works.

> **Labels on this page are from Crafty 4.10.8**, the version this project installs. If yours looks different, the words may have moved but the ideas are the same, and [Crafty's own documentation](https://docs.craftycontrol.com/) has current screenshots.

## Where everything is in Crafty

The **dashboard** is Crafty's front page — the list of your servers. Click a server's name and you land on its own page, with a row of tabs across the top. You will mostly live in the first four:

| Tab | What it is for |
| --- | --- |
| **Terminal** | The server talking to you, and the box where you type commands *to the server*. The most useful screen in Crafty. |
| **Files** | The server's own files, including `server.properties` where the game rules live. |
| **Config** | Crafty's settings for this server: name, port, whether it starts by itself. |
| **Player Management** | Kick, ban and unban players. |
| Backup | Make and restore backups. Step 5. |
| Schedule | Make things happen on a timer, like nightly backups. |
| Update Center | Change which Minecraft version this server runs. |

> **"Terminal" here is not the computer's terminal.** It is a box on a web page, and what you type goes to the Minecraft server, not to Linux. You cannot break the computer with it. This is where a few Minecraft things are done, because Crafty has no buttons for them.

On the Terminal tab, the server's output fills most of the page, and **below it** is an input box reading *Enter your command*. Type there and press Enter, or click **Send command**. The up arrow key brings back what you typed before.

To get back to the list of servers, use the dashboard link in Crafty's own menu.

## Creating the server

On the dashboard, the **All Servers** card has a **Create New Server** button in its top-right corner. That opens a wizard that walks you through a few screens, asking these:

| Field | First-time answer | Why |
| --- | --- | --- |
| **Server Type** and **Server Select** | **Paper** | A well-known Minecraft server flavour. Plays like normal Minecraft, runs smoothly, takes plugins later if you want them. |
| **Select a Version** | The version you play | The server and your game must match or you cannot join. See below. |
| **Server Name** | Something short, like `test` | Just a label inside Crafty. You can change it later. |
| **Server Port** | `25565` | The "door number" players connect to. The first server gets the standard one. |
| **Minimum Memory** | `1` (GB) | How much memory the server takes right away. |
| **Maximum Memory** | `3` (GB) | The most it is ever allowed to use. |

Memory is given in GB. More about the numbers on [Memory, ports and extra servers](../guides/server-sizing.md), and any unfamiliar word is in the [word list](../guides/glossary.md).

### Finding your Minecraft version

Open the Minecraft launcher and look at the version next to the **Play** button, or under **Installations**. Pick that same version in the wizard.

Getting this wrong is the single most common reason someone cannot join later, and the error they see says "outdated client" or "outdated server".

### The EULA

At some point a box appears titled **Agree To EULA**, asking whether you agree. That is Mojang's licence agreement, and every Minecraft server in the world has to accept it. Say yes, or the server will not start.

## Start it and watch the Terminal

The dashboard's server list has an **Actions** column on the right, with small icon buttons: **Start** when the server is stopped, and **Stop**, **Restart** and **Kill Process** when it is running.

Press **Start**, then open the server's **Terminal** tab and watch.

The first start is slow — the server is generating a world out of nothing. Wait for a line like `Done (34.5s)!`.

If it fills with red text and stops, do not panic: [When something breaks](../guides/troubleshooting.md).

## Join your own server

In Minecraft: Java Edition, click **Multiplayer** on the main menu, then **Add Server** at the bottom. Two boxes appear:

- **Server Name** is only a label for your own list. Call it anything.
- **Server Address** is the part that matters:
  - Playing on the same computer the server runs on: `localhost`
  - Playing on another computer at home: that computer's address, for example `192.0.2.10`

Click **Done**, then double-click the server in the list to join it. A green signal bar on the right means it answered; a red X means it did not.

Do not know the address? Ask whoever set the computer up. The port is on the server's **Config** tab as **Server Port** — if it is not `25565`, put it after a colon: `192.0.2.10:25566`.

You should now be standing in your own world. That is the whole thing working.

## Change how the world plays

The game rules live in a file called `server.properties`. To edit it:

**Files** tab → find `server.properties` in the file list → click it to open the editor → change the value after the `=` → click **Save Changes** → restart the server.

There is no separate settings screen for these; the file *is* the settings screen. The ones worth knowing early:

| Setting | Does what |
| --- | --- |
| `motd` | The line of text players see in their server list |
| `difficulty` | `peaceful`, `easy`, `normal` or `hard` |
| `gamemode` | `survival`, `creative`, `adventure` or `spectator` |
| `pvp` | Whether players can hurt each other |
| `max-players` | How many people can be online at once |
| `view-distance` | How far players can see. Lowering this is the easiest fix for a laggy server. |

Almost all of them need a restart before they do anything.

> **Careful with this file.** Change one line at a time and remember what you changed. If the server stops starting right after you edited it, the edit is your first suspect.

## Stop, start, restart

Use Crafty's buttons. Do not close the browser tab and switch the computer off — a Minecraft server keeps parts of the world in memory and writes them out when it shuts down properly. Cutting the power mid-write is how worlds get corrupted.

- **Stop** before you change files or do maintenance. It asks the server to shut down properly and save.
- **Restart** after settings changes.
- **Start** when it is stopped.
- **Kill Process** is not a normal button. It stops the server dead, without saving, and is only for a server that has frozen and will not respond to Stop. Treat it as the last resort it is.

## Changing things later

- **The Minecraft version** — the **Update Center** tab. Back up first; worlds do not always survive going backwards to an older version.
- **The name, port, or whether it starts by itself** — the **Config** tab.
- **The memory** — there are no memory boxes on Config. The numbers live inside the **Execution Command** line as `-Xms` (minimum) and `-Xmx` (maximum). If you are not comfortable editing that line, making a fresh server with better numbers is a perfectly reasonable answer.

## Making a second world

Two options, both fine:

- **A new world inside the same server** — same version, same settings, fresh terrain.
- **A brand new server** — better when you want a different Minecraft version, a different server type, or a mod pack. Old servers can sit there stopped, costing nothing but disk space.

<div class="pager" markdown="1">

- [← Step 2 — Set up Crafty](start-crafty.md)
- [Next: Step 4 — Invite your friends →](invite-friends.md)

</div>
