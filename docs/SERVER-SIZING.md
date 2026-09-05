# Server sizing and ports

This document gives practical defaults for small single-host Crafty installations.

The exact limits depend on the host, but the goal is to avoid giving every Minecraft server more resources than it can actually use.

## Memory defaults

For a normal Paper server with a few players:

```text
Minimum memory: 1 GB
Maximum memory: 3 GB
```

This is a good baseline for ordinary survival, creative play and light plugins.

For a somewhat heavier server:

```text
Minimum memory: 2 GB
Maximum memory: 4 GB
```

Use the larger values when there is an actual need, such as heavier plugins, larger view distances or a more demanding server setup.

## Why minimum and maximum are different

The Java process can start with a smaller heap and grow when needed.

Conceptually:

```text
Minimum = starting / lower memory target
Maximum = upper limit the server may use
```

For small servers, setting both values very high usually gives little benefit.

## Multiple servers

Several servers may exist in Crafty even if the host cannot run all of them at full load simultaneously.

For example, on a small host it may be perfectly reasonable to have:

```text
Survival   max 3 GB
Creative   max 3 GB
Testing    max 2 GB
```

if only one or two are normally running at once.

The important limit is the **combined memory usage of servers that are actually running**, plus memory needed by Linux, Docker and Crafty.

A useful rule is to leave clear headroom for the host operating system rather than allocating nearly all physical RAM to Minecraft heaps.

## CPU matters too

Minecraft server performance is often limited by CPU work rather than memory alone.

Common causes of lag include:

- generating new chunks;
- high view or simulation distance;
- many entities;
- expensive plugins;
- heavy modpacks;
- several busy servers running at once.

If a server lags, increasing RAM should not be the first automatic response.

## Port allocation

Each server that runs at the same time needs a unique listening port.

A simple convention is:

```text
25565  first server
25566  second server
25567  third server
25568  fourth server
```

The infrastructure administrator should reserve a specific range and expose only that range through the firewall/router when public access is required.

For example:

```text
25565-25575
```

would provide eleven possible Java server ports.

## Public addresses

The server using Java's default port `25565` can normally be entered as:

```text
minecraft.example.net
```

A server on another port is normally entered as:

```text
minecraft.example.net:25566
```

If separate friendly hostnames are desired, DNS SRV records can map names to different ports later.

## Practical recommendation

For a small family or friends server, start modestly:

```text
Paper
1 GB minimum
3 GB maximum
one unique port
whitelist enabled
```

Increase resources only when observed load or server behaviour justifies it.
