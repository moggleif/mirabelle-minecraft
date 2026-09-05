# Step 5 — Keep it safe

Worlds get lost. Someone blows up the base, a mod update eats the save, a disk dies, or you delete the wrong thing at midnight. A backup is what turns any of those from a disaster into an annoyance.

## Backups are not just for disasters

The real reason to back up is that it makes you brave. If you can undo anything in two minutes, you can try the risky mod, the big redstone build, the version upgrade. Without backups you end up too careful to have fun.

**Make a backup before you:**

- upgrade Minecraft to a new version
- change server type or install a mod pack
- add or update plugins
- try something you are honestly not sure about
- delete a server or a world

In Crafty that is the server's **Backup** tab. The **Backup Now!** button makes one immediately, and the list below shows the ones you already have, newest first.

And set up a scheduled backup for any world you would be sad to lose — the **Schedule** tab runs them on a timer, so you are not relying on remembering.

## Three layers, three different problems

```text
Git             -> the recipe: compose.yaml, docs, settings examples
Crafty backups  -> undo button for one world or one server
Off-host copy   -> survives the computer itself dying
```

They are not interchangeable. This is the single most common misunderstanding, so it is worth saying plainly:

> **GitHub does not have your world.** The project in Git describes *how to build the server*. Your actual world lives in the data folder on the host and is never uploaded. If you only have Git, and the computer dies, you have the blueprint and no house.

## Copying files by hand is not a backup

A running Minecraft server is constantly writing to the world files. Copy them mid-write and you may get a world that looks fine and then breaks later.

So: either stop the server first, or use Crafty's backup feature, which knows how to do this properly. Do not drag world folders around while people are playing.

## Get a copy off the computer

Crafty's backups land on the same machine as the server. That protects you from mistakes, not from the machine.

Copy the backup folder somewhere else as well — another computer, a NAS, an external disk, cloud storage. Anything that will not be in the room when the host's disk fails.

> **The test:** if this computer disappeared right now, would your world still exist somewhere? If the answer is no, you have one layer, not three.

## Restoring one server

1. Stop the server if it is still running.
2. Open its **Backup** tab and pick a backup you trust from the list — ideally one made before whatever went wrong. The dates are your evidence.
3. Restore it using the restore button on that row.
4. Start the server.
5. Read the **Terminal** tab for errors.
6. Join it and actually look around before telling everyone it is fixed.

## Rebuilding the whole host

If the machine is gone and you are starting on a new one:

1. Install Docker and Git.
2. Clone this project.
3. `cp .env.example .env` and set the paths for the new machine.
4. Restore the Crafty data folder from your off-host copy.
5. Check the folder is owned by the right user.
6. `docker compose config` to check the recipe.
7. `docker compose up -d` to start it.
8. Log in to Crafty and check your servers and worlds.
9. Redo any router, DNS or proxy settings.

The project rebuilds the *setup*. The off-host copy rebuilds the *worlds*. You need both.

## Try a restore before you need one

A backup you have never restored is a guess. Once — right now is a good time — restore a backup onto a throwaway server and see that it works. Then you know, instead of hoping.

<div class="pager" markdown="1">

- [← Step 4 — Invite your friends](../getting-started/invite-friends.md)
- [Next: When something breaks →](../guides/troubleshooting.md)

</div>
