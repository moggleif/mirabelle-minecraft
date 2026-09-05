# Server sizing and ports

Minecraft server memory should be sized for the workload rather than simply given as much RAM as possible.

## Practical starting point

For a small Paper server with a few players, start conservatively:

- minimum memory: 1 GB
- maximum memory: 3 GB

For a somewhat heavier plugin setup, 2 GB minimum and 4 GB maximum can be reasonable if the host has enough memory.

More RAM does not automatically make Minecraft faster. CPU performance, chunk generation, view distance, plugins and mods can matter more.

## Multiple servers

Several servers may be configured in Crafty, but the host needs enough memory for the servers that are actually running at the same time plus Docker, Crafty and the operating system.

Do not allocate the entire host's RAM to Minecraft JVM maximum values.

If servers are normally used one at a time, each can have a useful maximum without all of those maxima needing to fit simultaneously. If several are intended to run together, size them as a group.

## Minimum versus maximum memory

The minimum value is roughly the memory Java starts with or reserves as its initial heap target. The maximum is the upper limit the Minecraft JVM may grow to.

A useful default for a small server is therefore:

```text
Minimum: 1 GB
Maximum: 3 GB
```

Change it only when the server workload gives you a reason to do so.

## Ports

Every simultaneously running Minecraft server on the same host needs its own listening port.

A simple allocation is:

```text
first server   25565
second server  25566
third server   25567
...
```

Keep the externally exposed range small. The Compose deployment uses a configurable Java range so the administrator can decide how many ports are available.

The default Minecraft Java port is 25565. Players can connect to the default port using only the hostname; servers on another port normally require `hostname:port` unless DNS SRV records are configured.

## Choosing server software

Paper is a good first choice for a server that should feel close to vanilla Minecraft while allowing performance improvements and plugins.

Different server types and modpacks can have very different memory and CPU requirements, so treat the values above as starting points rather than guarantees.

## When to increase memory

Consider increasing the maximum only when you have evidence that the server is memory constrained, for example sustained heap pressure or workload requirements from a known modpack/plugin set.

Do not use extra RAM as the first response to every performance problem. Check CPU load, server timings, chunk generation and plugin behaviour as well.
