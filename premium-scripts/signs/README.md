---
description: >-
  Real-time 3D sign creator for FiveM — admins place persistent text signs in the
  world using Lith 3D font packs, with in-world gizmo editing and database sync.
---

# Real-Time 3D Signs

## Overview

`ls_signs` adds a real-time 3D sign creator to your FiveM server. Admins place persistent text signs in the world using Lith 3D font packs. Every player sees the same signs; each client spawns local glyph props streamed by distance.

Players and admins can:

* See 3D text signs placed around the map (streamed in by distance)
* Toggle sign visibility client-side with `/cd` (useful for screenshots or performance checks)
* **Admins only:** Open the sign creator with `/signs`, place new signs, edit existing ones, or delete them
* **Admins only:** Hot-reload the font list with `/refreshfonts` after starting or stopping font resources (no `ls_signs` restart needed)

This resource is **standalone** — no ESX, QBCore, or framework dependency.

Main files:

* `config.lua` — admin access, editor limits, layout defaults ([Configuration](./config.md))
* `locale.lua` — player-facing strings ([Locale | Translations](./locale-or-translations.md))
* `server/editables.lua` — admin permission hook ([Configuration](./config.md#servereditableslua-full-file))
* `server/server.lua` — database persistence and sign sync (auto-creates the `ls_signs` table on first start)
* `client/` — font discovery, 3D rendering, gizmo editor, NUI creator panel
* `web/` — sign creator UI (HTML/CSS/JS; shipped pre-built)

## Installation

{% stepper %}
{% step %}

### Place the resource

Put the `ls_signs` folder in your server resources directory (e.g. `/resources/[lith]/ls_signs/`).
{% endstep %}

{% step %}

### Install dependencies

* **[oxmysql](https://github.com/overextended/oxmysql)** — required; `ls_signs` stores signs in MySQL/MariaDB.
* **Lith 3D font packs** — shipped as **separate resources** in the same [portal.cfx.re](https://portal.cfx.re) download as `ls_signs` (e.g. `bebasneue_text`, `montserrat_text`). Copy each font folder into your resources directory and `ensure` the packs you want. Each declares `text3d_font '<key>'` in its manifest; only **started** fonts appear in the creator dropdown.

{% hint style="info" %}
You do not download fonts separately — they are included with the script package on the CFX portal. Install only the font resources you plan to use.
{% endhint %}

{% hint style="warning" %}
Without at least one started font resource, the creator has no fonts to choose from. The default font key in `config.lua` (`bebasneue`) must match a discovered `text3d_font` key.
{% endhint %}
{% endstep %}

{% step %}

### Configure admin access

Grant the ACE permission in `server.cfg`. The shipped `server/editables.lua` checks `Config.acePermission` by default — customize it only if you use a different admin system.

```cfg
add_ace group.admin ls_signs.admin allow
```

See [Access](./config.md#access) for keybind and custom permission examples.

{% endstep %}

{% step %}

### Ensure in server.cfg

Start font packs **before** `ls_signs`, then ensure the main resource:

```cfg
ensure bebasneue_text
ensure ls_signs
```

Add more `ensure <font>_text` lines for every font pack you install.
{% endstep %}

{% step %}

### Restart and verify

* Restart the server or run `refresh` then `ensure ls_signs`
* Check the console for `[ls_signs] Loaded N sign(s)` and no database errors
* As an admin, run `/signs` and confirm the creator opens with at least one font in the list
{% endstep %}
{% endstepper %}

{% hint style="info" %}
No manual SQL import is required. The server creates the `ls_signs` table automatically on first boot.
{% endhint %}

## Font packs

3D glyphs are provided by **separate font resources**, not by `ls_signs` itself. When you download `ls_signs` from [portal.cfx.re](https://portal.cfx.re), the package includes one or more `*_text` font resources alongside the main script.

* Place each font folder in your resources directory (same as `ls_signs`).
* Add `ensure <font>_text` lines to `server.cfg` **before** `ensure ls_signs`.
* You only need to start the fonts you want in the creator — unused packs can stay on disk unstarted.

### Hot-reload fonts with `/refreshfonts`

After the server is running, admins can add or remove fonts **without restarting `ls_signs`**:

1. `ensure` a new font resource, or `stop` one you no longer want.
2. Run `/refreshfonts` in-game (admin only).

The command re-scans started font resources and updates the creator's font dropdown immediately. Stopped fonts drop out of the list; newly started fonts become available for new and edited signs.

{% hint style="info" %}
`/refreshfonts` is per-client for the creator UI. Each admin should run it after font changes if they already have the creator open. New players pick up the current font list on join automatically.
{% endhint %}

## Configuration

All tuning is in `config.lua` and `server/editables.lua`. See [Configuration](./config.md) for the full default files and a tuning guide for editor limits and layout.

## Gameplay flow

{% stepper %}
{% step %}

### Admin opens the creator

Run `/signs` (or your configured keybind). If signs exist within `Config.nearbyDistance` metres, a picker lists them to edit; otherwise a new sign session starts in front of the player.
{% endstep %}

{% step %}

### Place and style the sign

Use the NUI panel to enter text, pick a font and colours, toggle the background panel, and adjust scale, line spacing, and panel size. Move and rotate the sign with the in-world gizmo and editor camera. A live preview renders as you work.
{% endstep %}

{% step %}

### Save

Saving sends the sign to the server, which validates the payload, writes to the database, and broadcasts the updated list to all clients. Signs persist across restarts.
{% endstep %}

{% step %}

### Players see signs in the world

Each client streams signs within 250 m, spawning local 3D glyph props. Players can hide signs locally with `/cd` without affecting others.
{% endstep %}
{% endstepper %}

## Troubleshooting

### Creator says no permission

* Confirm `add_ace … ls_signs.admin allow` is in `server.cfg`
* Confirm `server/editables.lua` returns `true` for your admin check (default: `IsPlayerAceAllowed` with `Config.acePermission`)
* Restart the resource after editing `editables.lua`

### No fonts in the dropdown

* Font packs are **separate resources** from the same [portal.cfx.re](https://portal.cfx.re) download — copy and `ensure` at least one `*_text` pack before `ls_signs`
* After starting or stopping a font at runtime, run `/refreshfonts` as an admin to update the dropdown without restarting `ls_signs`
* Set `Config.defaultFont` to a key that matches an installed font's `text3d_font` metadata

### Signs not visible

* Run `/cd` — signs may be toggled off locally
* Move closer; default render distance is 250 m
* Check the server console for load errors and confirm signs exist in the `ls_signs` database table

### Database errors

* Confirm **oxmysql** is installed and configured with a valid connection string
* Check that the MySQL user can `CREATE TABLE` (first boot) and read/write `ls_signs`
