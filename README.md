# FiveMod Installer

**Install any FiveM mod by dragging it in. No manual file edits, no broken servers, one-click undo.**

### [⬇ Download the latest version](https://github.com/bb-npcore/fivemod-releases/releases/latest)

Windows · 64-bit · signed installer

---

## What it's for

Every FiveM mod ships with its own install instructions, and they all assume you already know things most server owners don't.

A typical script README says:

> 1. Drag the resource into your resources folder
> 2. Add the items to your shared items
> 3. Add the images to your inventory
> 4. Import the SQL file
> 5. Add `ensure scriptname` to server.cfg
> 6. Configure config.lua

Six lines. Here's what they actually mean.

**"Add the items to your shared items."** Where, and in what format? That depends on your framework *and* your inventory — and each combination wants a different file in a different shape. QBCore expects one thing, ox_inventory another, ESX puts them in the database instead. Wrong format breaks the Lua file. Wrong location and nothing happens at all.

**"Add the images."** Six common inventories, six different image folders. Wrong one and your items show up blank — no error, no warning, just silently broken.

**"Import the SQL file."** Assumes you have a SQL client, can find your database credentials, and know what to do when a table already exists or a premium script wants to `ALTER` a core table three other scripts depend on. Run it twice, get duplicates. Run the wrong one, there's no undo.

**"Add ensure to server.cfg."** Order matters. Dependencies have to start before the things that use them. Put the line in the wrong place and the script loads fine, then fails at runtime with nothing in the console pointing at why.

And that's a *simple* script. Premium ones replace your framework, delete your existing inventory, run framework-specific SQL, wire up API keys — ten-plus steps where one mistake breaks the server.

**Then the real problem: there's no undo.** Files are now spread across several directories, items are mixed into a shared file alongside hundreds of others, SQL tables exist, server.cfg is edited, images are scattered. Unwinding that by hand is miserable, so most people restore a full server backup and lose every other change they made — or just live with the broken install.

That is the single biggest reason people give up on running a FiveM server.

---

## What this does instead

**You drag the mod in. The app does the rest.**

1. **Reads your server first** — detects your framework, inventory, database and what's already installed, so every decision is based on your actual setup instead of a guess.
2. **Works out what the mod needs** — items, images, dependencies, SQL, config changes, start order — read from the mod's own files, in whatever format the author used.
3. **Shows you the plan before touching anything** — every file, item, SQL statement and `server.cfg` line. Nothing is written until you approve it.
4. **Checks for conflicts first** — item names you already have, tables that already exist, missing dependencies, clashing resources. You find out before the install, not when the server won't boot.
5. **Installs it properly** — files in place, items written in your framework's exact format, images in the right inventory folder, SQL run against your database, `server.cfg` updated in the correct position.
6. **Records everything it changed**, per mod, down to the individual file and SQL statement.
7. **One-click uninstall** — because it tracked the changes, it can reverse them, pulling out just that mod's items, files, images and tables and leaving everything else exactly as it was.

That last point is the part no manual process gives you.

---

## What it handles

| Mod type | Handled |
|---|---|
| Vehicles / car mods | Resource placement, stream files, `server.cfg` entry |
| Scripts | Files, items, images, SQL, config, dependencies, start order |
| Premium / complex scripts | Guided install with backups, framework changes, database migrations |
| MLOs | Resource placement, streaming assets, `server.cfg` entry |
| Maps | ymap / ytyp handling and correct load order |

**Frameworks:** QBCore · ESX · QBox · standalone
**Inventories:** ox_inventory · qb-inventory · esx_inventory · qs-inventory · lj-inventory · core_inventory

Item definitions get converted into whatever format your setup actually uses, so a mod written for one framework still installs correctly on another.

---

## Safety

Breaking a live server is the thing people are most afraid of, so the app is built around that.

- **Preview before every change** — nothing is written until you've seen exactly what will happen
- **Backups on every install**, with a restore point you can return to
- **Per-mod revert** — remove one mod's changes without disturbing anything else
- **Conflict detection up front** — duplicate items, existing tables, missing dependencies, clashing resources
- **Change history** — a record of what was installed and what each install touched

Escrow-protected script code stays encrypted end to end. The app reads only what your FiveM server itself can read: manifests, configs and item definitions.

---

## Install

1. [Download the latest `.exe`](https://github.com/bb-npcore/fivemod-releases/releases/latest)
2. Run it. Windows SmartScreen may warn on a new release — choose **More info → Run anyway**.
3. Open the app and follow the Setup Wizard to point it at your server folder.

The `.sig` file next to each download is the update signature. You don't need to download it — the app uses it to verify updates.

**Updates are automatic.** The app checks this repository on launch and updates itself when a new version is published.

---

## Requirements

- Windows 10 or 11, 64-bit
- A FiveM server you have file access to
- MySQL / MariaDB reachable from your machine, for mods that ship SQL
- An active licence
- An internet connection for licence checks and mod analysis

---

## Releases

All versions live on the [Releases page](https://github.com/bb-npcore/fivemod-releases/releases). Latest is **v0.1.1**.

This repository hosts release builds only — it contains no source code. FiveMod Installer is commercial software.

---

## Support

Found a bug or need help with an install? Open an [issue](https://github.com/bb-npcore/fivemod-releases/issues) with your version number and what you were installing when it happened.

---

*Not affiliated with Cfx.re or FiveM. Framework and script names belong to their respective authors.*
