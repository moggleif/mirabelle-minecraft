# Step 2 — Set up Crafty

This is the only part of the guide with real terminal work. Take it slowly, one command at a time, and read what comes back before typing the next one.

> **First time in a terminal?** A terminal is a window where you type commands instead of clicking. You type one line, press Enter, and the computer answers. Nothing happens until you press Enter, so it is safe to read a command twice before you commit.

## What the commands look like

Command blocks on this site look like this:

```bash
whoami
```

Type it (or copy it), press Enter, done. Some commands need administrator rights, and those start with `sudo`. That word means *do this as the computer's administrator* — the computer will ask for a password, and nothing will appear on screen while you type it. That is normal.

## 1. Copy the project onto the host

Do this on the computer that will run the server.

```bash
git clone https://github.com/moggleif/mirabelle-minecraft.git
cd mirabelle-minecraft
```

`git clone` downloads the project. `cd` moves you into the folder it created. Every command after this assumes you are standing in that folder.

## 2. Make your settings file

The project ships an example settings file. You copy it and edit your copy:

```bash
cp .env.example .env
```

Open `.env` in a text editor (`nano .env` works everywhere) and check these four lines:

| Setting | What it means |
| --- | --- |
| `CRAFTY_DATA_DIR` | The folder where your worlds and backups will live. Keep it outside the project folder. |
| `TZ` | Your time zone, so scheduled backups happen at the hour you expect. For example `Europe/Stockholm`. |
| `CRAFTY_HTTPS_PORT` | The port you will use to reach the Crafty website. `8443` is fine. |
| `MC_JAVA_PORT_RANGE` | The ports your Minecraft servers may use. `25565-25575` is fine. |

In nano, save with `Ctrl+O` then Enter, and leave with `Ctrl+X`.

> **`.env` stays on this computer.** It is deliberately ignored by Git, and it should never be uploaded anywhere. See [Public repository safety](../project/public-repo-safety.md).

## 3. Create the data folder

Make the folder you named in `CRAFTY_DATA_DIR`, and make yourself its owner:

```bash
sudo mkdir -p /srv/crafty
sudo chown -R "$USER":"$USER" /srv/crafty
```

Replace `/srv/crafty` if you chose a different path.

## 4. Check the recipe, then start Crafty

First, ask Docker to read the recipe and tell you whether it makes sense. This changes nothing:

```bash
docker compose config
```

If that prints a wall of settings without an error, start Crafty:

```bash
docker compose pull
docker compose up -d
```

`pull` downloads Crafty. `up -d` starts it in the background (`-d` is for *detached*, meaning it keeps running after you close the terminal).

Check that it is alive:

```bash
docker compose ps
docker compose logs --tail=50
```

The first start takes a couple of minutes. Crafty is unpacking itself and setting up its database.

## 5. Find your first password

The first time Crafty starts, it makes an admin account for you and generates a random password. It writes that password into a file called `default-creds.txt` in its config folder, and also mentions it in the startup output.

```bash
cat /srv/crafty/config/default-creds.txt
```

If the file is not there yet, wait a minute and try again — Crafty may still be starting. You can also search the startup output:

```bash
docker compose logs | grep -i -A2 password
```

Write the password down somewhere for the next two minutes. You are about to change it anyway.

## 6. Open Crafty in your browser

On the host itself:

```text
https://localhost:8443
```

From another computer on the same network, use the host's address instead of `localhost`, for example `https://192.0.2.10:8443`. If you do not know it, run `hostname -I` on the host.

**Your browser will warn you that the connection is not private.** This is expected. Crafty makes its own security certificate, and your browser has no way to know it is trustworthy — the same way it would not trust a passport you printed at home. On your own network, click through the warning (usually *Advanced* → *Continue*).

Log in with `admin` and the password from step 5.

## 7. Change the password immediately

In Crafty, open your user profile and set a real password. Then delete the file with the old one:

```bash
rm /srv/crafty/config/default-creds.txt
```

> **Password advice, briefly:** make it long, make it unique to Crafty, and do not send it to friends. Anyone with your Crafty password can delete every world you have.

## Done

Crafty is running and it is yours. Nothing is playable yet — that is the next page.

If any of this went sideways, [When something breaks](../guides/troubleshooting.md) covers the usual failures.

---

**Next:** [Your first server](first-server.md)
