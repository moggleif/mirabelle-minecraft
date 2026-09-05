# Memory, ports and extra servers

Two numbers confuse everyone at the start: how much memory to give a server, and which port to put it on. Here are answers you can just use.

## Memory: what to type

For a normal Paper server with a few friends on it:

```text
Minimum memory: 1 GB
Maximum memory: 3 GB
```

For something heavier — a mod pack, lots of plugins, a bigger group:

```text
Minimum memory: 2 GB
Maximum memory: 4 GB
```

Start with the first one. Move up only when you have an actual reason.

## Why there are two numbers

**Minimum** is how much memory the server grabs when it starts. **Maximum** is the ceiling it is never allowed to cross.

```text
Minimum = what it takes straight away
Maximum = the most it may ever take
```

Setting both to something huge does not make Minecraft faster. It just means the server can eat memory the rest of the computer needs.

## More memory is usually the wrong fix

If your server is laggy, memory is rarely the cause. Minecraft mostly struggles with *work*, not space:

- generating new terrain when someone explores fast
- a high view distance or simulation distance
- thousands of mobs, items or hoppers
- expensive plugins or a big mod pack
- several servers running at once on one machine

Lower the view distance first. It costs you almost nothing and helps more than a memory bump.

## Running more than one server

You can create as many servers in Crafty as you like. What matters is how many run **at the same time**, because only running servers use memory.

So this is perfectly reasonable on a small machine:

```text
Survival   max 3 GB
Creative   max 3 GB
Testing    max 2 GB
```

as long as you only ever have one or two of them started.

Leave clear headroom for Linux, Docker and Crafty themselves. Handing almost all the machine's memory to Minecraft is how you get a host that freezes instead of a server that runs fast.

## Ports: one door each

Every server that runs at the same time needs its own port. Count upwards:

```text
25565  first server
25566  second server
25567  third server
25568  fourth server
```

`25565` is Minecraft's standard port, so the server sitting on it can be reached without typing a port at all:

```text
minecraft.example.net
```

Anything else needs the port spelled out:

```text
minecraft.example.net:25566
```

This project reserves a small range in `.env`:

```text
MC_JAVA_PORT_RANGE=25565-25575
```

That is eleven possible servers, which is plenty. Stay inside the range when you create servers, and do not widen it just in case — every open port is another door to look after.

## A good starting point

If you want one set of settings to copy for your first real server:

```text
Paper
1 GB minimum
3 GB maximum
port 25565
whitelist on
view-distance 10
```

Adjust once you have watched it run with people on it. Guessing in advance is not worth the effort.

---

**See also:** [Host and Docker notes](../operations/deployment.md) for opening those ports on the network.
