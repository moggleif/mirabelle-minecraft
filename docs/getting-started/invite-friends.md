# Step 4 — Invite your friends

A server with nobody on it is just a very slow single-player world. This page is about letting the right people in and keeping everyone else out.

## Turn the whitelist on first

A **whitelist** is a guest list. If your name is on it you can join; if it is not, the server turns you away without you having to ban anyone.

Turn it on *before* anyone else gets the address. It is set per server, not once for all of Crafty. In that server's `server.properties`:

```properties
white-list=true
enforce-whitelist=true
```

The second line matters: it kicks out anyone already online who is not on the list, instead of only checking at the door.

Then add people. In Crafty's player screens, or by typing this in the server console:

```text
whitelist add PlayerName
```

Use their exact Minecraft username. To remove someone:

```text
whitelist remove PlayerName
```

> **Whitelist beats banning.** A ban is for someone you let in and regret. A whitelist means you never had to.

## Who gets to be an admin

An **operator** (or "op") can use cheat-level commands: change the weather, teleport, give themselves items, kick people. Ops can also op other people.

Give it to nobody at first, including yourself, unless you actually need it. It is easy to add and awkward to take back after somebody has filled the world with TNT.

In the console:

```text
op PlayerName
deop PlayerName
```

Crafty accounts are a separate thing entirely. A Crafty login can create and delete whole servers, so keep those to people who are actually running the machine with you.

## The address you give people

**Friends on your home network** use the host's local address, for example `192.0.2.10`. Nothing else needed.

**Friends somewhere else** need your home network to let them in from the internet. Someone has to open a port on the router and point it at the host. That is a real change to your home network's security, so:

> **Ask the person who owns the router before you open anything.** Show them this page. Opening a port means anyone on the internet can knock on that door, and you want an adult to know that door exists.

If you do open it, open only the Minecraft port range, and only that. The details are on [Host and Docker notes](../operations/deployment.md).

Two rules that are not optional:

- **Never expose Crafty's web port (`8443`) to the internet.** Crafty can delete every world you have. It belongs on your home network or behind a VPN.
- **Leave `online-mode=true`.** It is what checks that a player is really who their username says. Turning it off lets anyone log in as anyone.

## Ports, briefly

Every server that runs at the same time needs its own port. The standard Minecraft port is `25565`, and a server on that port needs no port in its address:

```text
minecraft.example.net
```

Anything else has to be typed out:

```text
minecraft.example.net:25566
```

If you later want friendly names without port numbers, that is what DNS SRV records are for. Not something you need on day one.

## Ground rules are worth writing down

Whoever is on your server is on your computer, in your world. It is entirely reasonable to say out loud what is and is not okay — griefing, stealing, who can use ops, who gets to invite people. Doing it early is easier than doing it after an argument.

And if someone will not stop:

```text
kick PlayerName
ban PlayerName
```

Or just take them off the whitelist. It is your server.

---

**Next:** [Keep it safe](../operations/backup-recovery.md)
