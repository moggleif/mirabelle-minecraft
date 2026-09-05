# When something breaks

Something will break. That is not a sign you did it wrong — it is the normal state of running a server. Almost everything on this page is a five-minute fix.

**Jump to your problem:**

- [The Crafty website will not open](#the-crafty-website-will-not-open) — *needs the computer*
- [The browser says the connection is not private](#the-browser-says-the-connection-is-not-private)
- [I lost the Crafty password](#i-lost-the-crafty-password) — *needs the computer*
- [A Minecraft server will not start](#a-minecraft-server-will-not-start)
- [A friend cannot join](#a-friend-cannot-join)
- [Everything is laggy](#everything-is-laggy)
- [Permission denied about the data folder](#permission-denied-about-the-data-folder) — *needs the computer*
- [Crafty keeps restarting on its own](#crafty-keeps-restarting-on-its-own) — *needs the computer*
- [Nothing here helps](#nothing-here-helps)

> **Two kinds of fix.** Most of these you do in Crafty, in your browser. The ones marked *needs the computer* mean typing in a terminal on the machine that runs the server. If that is not your computer, this is the moment to ask whoever set it up rather than guessing.

## How to look at an error

Two habits will solve most problems on their own:

1. **Read the first error, not the last one.** When something fails, it usually fails once and then complains about the consequences twenty more times. The top of the red text is the real story.
2. **Change one thing, then test.** If you change four things and it works, you have learned nothing and you cannot undo it cleanly.

Where to look:

- **A Minecraft server misbehaving** → open that server in Crafty and read the **Terminal** tab. Everything the server says goes there, and the **Logs** tab keeps the older lines.
- **Crafty itself misbehaving** → the terminal on the computer, in the project folder:

```bash
docker compose ps
docker compose logs --tail=100
```

## The Crafty website will not open

Check that the container is actually running:

```bash
docker compose ps
```

If nothing is listed, or the state is not `running`, start it and read what it says:

```bash
docker compose up -d
docker compose logs --tail=100
```

Then work down this list:

- Are you using `https://` and not `http://`? Crafty only speaks HTTPS.
- Is the port right? It is whatever `CRAFTY_HTTPS_PORT` says in `.env` — `8443` unless you changed it.
- From another computer, are you using the host's address and not `localhost`? `localhost` always means *this* computer.
- Is the host's firewall blocking the port? On a home network, allowing it on the local network is fine.

## The browser says the connection is not private

Expected. Crafty makes its own certificate, and browsers do not trust homemade certificates. On your own network, click through the warning.

If you want a proper padlock and a real hostname, that is a reverse proxy job — see [Host and Docker notes](../operations/deployment.md).

## I lost the Crafty password

If you never changed it, it is still in the config folder:

```bash
cat /srv/crafty/config/default-creds.txt
```

If you did change it and forgot it, Crafty's [own documentation](https://docs.craftycontrol.com/) has the password reset procedure. That is their tool, so use their instructions rather than guessing.

## A Minecraft server will not start

Open the server's **Terminal** tab in Crafty and look for one of these.

**The EULA is not accepted.** Every Minecraft server has to agree to Mojang's licence. Accept it in Crafty and start again.

**Something about failing to bind, or the address already being in use.** Two servers are trying to use the same port. Change one of them: the server's **Config** tab → **Server Port** → save → start again. See [Memory, ports and extra servers](server-sizing.md).

**Out of memory, or the server dies silently while starting.** The maximum memory is too low, or the computer has run out. Stopping another running server is the quick fix; changing the memory itself means editing the **Execution Command** on the **Config** tab, or making a fresh server with better numbers.

**Complaints about Java or the version.** Newer Minecraft versions need newer Java, and older ones sometimes need older Java. Match the Minecraft version to what your players actually have, and check what that version needs.

**The disk is full.** Worlds, backups and logs grow. Check with:

```bash
df -h
```

Old backups and stopped test servers are usually the easiest things to delete.

## A friend cannot join

Go through it in this order — the answer is almost always in the first three:

1. **Are they on the whitelist?** Exact username, correct spelling. Check with `whitelist list` in the server's **Terminal** tab.
2. **Is their Minecraft version the same as the server's?** "Outdated client" or "outdated server" means exactly this.
3. **Are they using the right address, with the port if it is not `25565`?**
4. **Are they at home with you, or somewhere else?** From outside your network they need a forwarded port. See [Invite your friends](../getting-started/invite-friends.md).
5. **Is the server actually running?** Check Crafty. It is worth ruling out.

## Everything is laggy

Lag is usually the computer working too hard, not the server needing more memory. Adding memory is the most common wrong first move.

Try, in this order:

- Lower `view-distance` (try `8`, or `6`). This is by far the biggest win. **Files** tab → `server.properties` → change it → save → restart.
- Lower `simulation-distance` in the same file.
- Stop any other Minecraft servers that are running.
- Look for what is causing it: huge farms, thousands of mobs or items on the ground, a heavy plugin, or the world generating brand new terrain because someone is exploring fast.

Only then think about memory. And if the host is an old laptop, there is a limit to what settings can fix.

## Permission denied about the data folder

Crafty could not write to its own files. Give the folder back to your user:

```bash
sudo chown -R "$USER":"$USER" /srv/crafty
docker compose restart
```

Use your real `CRAFTY_DATA_DIR` path if it is not `/srv/crafty`.

## Crafty keeps restarting on its own

Read the logs — the reason is in there, usually near the first error:

```bash
docker compose logs --tail=200
```

Common causes: the data folder does not exist, the data folder is not writable, or the port is already used by something else on the host.

## Nothing here helps

Then it is worth asking for help, and how you ask decides whether you get an answer:

- What you were doing when it broke.
- What you expected, and what actually happened.
- The first few lines of the error, copied as text.
- What you already tried.

Crafty questions belong with [Crafty's own project](https://docs.craftycontrol.com/). Problems with *this* setup — the compose file, these docs — belong in [this project's issues](https://github.com/moggleif/mirabelle-minecraft/issues).

> **Before you paste logs anywhere public,** skim them for your home IP address, hostnames, usernames or anything that looks like a password. Swap those for `example` values.

<div class="pager" markdown="1">

- [← Step 5 — Keep it safe](../operations/backup-recovery.md)
- [Word list: what the words mean →](glossary.md)

</div>
