# Config

Server-owner tuning for `ls_signs` lives in `config.lua` at the resource root and `server/editables.lua` for admin permissions. After any change:

```cfg
refresh
ensure ls_signs
```

NUI strings are in `locale.lua` — see [Locale](./locale-or-translations.md). The sign creator UI (`web/`) is shipped pre-built; you only need to rebuild if you modify the web source yourself.

## config.lua (full file)

Complete default config as shipped. Edit this file in your resource folder.

```lua
Config = {}

-- Debug prints
Config.debug = false

--------------------------------------------------------------------------------
-- Access
--------------------------------------------------------------------------------

-- Ace permission required to open the sign creator and create/edit/delete signs.
-- Grant in server.cfg, e.g:   add_ace group.admin ls_signs.admin allow
Config.acePermission = 'ls_signs.admin'

-- Command + suggested keybind to open the creator (admins only; enforced server-side too)
Config.openCommand = 'signs'
Config.openKeybind = '' -- e.g. 'F7' to register a key mapping, '' to disable

-- Chat command any player can use to toggle sign visibility locally (on by default).
-- Set to '' to disable the command entirely.
Config.toggleCommand = 'togglesigns'

--------------------------------------------------------------------------------
-- Rendering
--------------------------------------------------------------------------------

-- Distance (metres) at which a sign's glyphs spawn / despawn around the player.
Config.renderDistance = 150.0

-- How often (ms) the distance loop re-evaluates which signs should be spawned.
Config.streamInterval = 750

-- Default font key used when the creator opens (must match a discovered text3d_font).
Config.defaultFont = 'bebas'

-- Maximum number of characters allowed in a sign's text (enforced in the creator
-- and again server-side on save). Default 20, hard-capped at 256.
Config.maxTextLength = 30

--------------------------------------------------------------------------------
-- Editor
--------------------------------------------------------------------------------

-- Max distance (metres) from the player the sign proxy can be moved during placement.
Config.editorMaxDistance = 150.0

-- Radius (metres) used when /signs lists nearby signs before opening the creator.
Config.nearbyDistance = 50.0

--------------------------------------------------------------------------------
-- Layout
--------------------------------------------------------------------------------

-- Vertical gap between lines, in font units (multiplied by the sign's scale).
Config.lineGap = 1.15

-- Padding added around the text block when auto-sizing the background panel,
-- in font units (x = horizontal, y = vertical).
Config.panelPadding = { x = 0.25, y = 0.25 }

-- Depth offset (font units) the panel sits behind the glyphs along the sign's
-- local forward axis.
Config.panelDepth = 0.03

-- Background-panel size sliders in the creator are multipliers on the auto-sized
-- layout bounds (1.0 = fit text + padding). Clamped server-side on save.
Config.panelSizeRange = { min = 0.5, max = 3.0, step = 0.05, default = 1.0 }

--------------------------------------------------------------------------------
-- Database
--------------------------------------------------------------------------------

-- 'oxmysql' | 'mysql-async'
Config.sqlDriver = 'oxmysql'
```

## server/editables.lua (full file)

Complete default admin hook as shipped. Edit this file to connect your permission system.

```lua
function isAdmin(src)
    return IsPlayerAceAllowed(src, Config.acePermission)
end
```

{% hint style="info" %}
The default checks ACE via `Config.acePermission`. Replace the function body if you use a framework admin check or custom permission system instead.
{% endhint %}

## Tuning guide

### Access

Controls who can open the sign creator and create, edit, or delete signs.

* `Config.acePermission` — ACE string checked server-side on every write. Grant with `add_ace group.admin ls_signs.admin allow` (or your group/identifier).
* `Config.openCommand` — Chat command that opens the creator (default `signs`). Client-side UX gate only; the server still validates admin status on save.
* `Config.openKeybind` — Optional FiveM key mapping (e.g. `'F7'`). Leave `''` to disable. Label comes from `locale.lua` (`keybind.open_creator`).
* `Config.toggleCommand` — Chat command any player can use to hide or show signs **on their own client** (default `togglesigns`). Signs are visible on join. Set to `''` to disable the command. Does not affect other players or admin editor previews.
* `server/editables.lua` — `isAdmin(src)` must return `true` for allowed players. Wire to ACE, framework jobs, or your admin menu.

**Example:** Grant ACE to admins and bind F7 to open the creator:

```cfg
add_ace group.admin ls_signs.admin allow
```

```lua
Config.openKeybind = 'F7'
```

**Example:** Rename the visibility toggle for your community:

```lua
Config.toggleCommand = 'hidesigns'
```

### Rendering

Controls how far signs stream in and how often the client re-checks distance.

* `Config.renderDistance` — Metres at which sign glyphs spawn/despawn around each player. Lower values reduce prop count and may help performance in sign-heavy areas.
* `Config.streamInterval` — Milliseconds between distance checks. Lower values react faster when moving; higher values reduce CPU use.
* `Config.defaultFont` — Font key pre-selected when the creator opens. Must match a started resource's `text3d_font` metadata. Font packs are **separate resources** included in the [portal.cfx.re](https://portal.cfx.re) download — see [Font packs](./README.md#font-packs).
* `Config.maxTextLength` — Character limit in the creator and on server save. Hard-capped at `256` regardless of config. Shorter limits reduce glyph prop count per sign.
* `Config.debug` — Logs font discovery and other diagnostics to the client/server console. Leave `false` on production.

After starting or stopping font resources at runtime, admins can run `/refreshfonts` to hot-reload the creator's font list without restarting `ls_signs`.

{% hint style="info" %}
Signs use client-local glyph props (not networked entities). Each player toggles visibility independently with `Config.toggleCommand`.
{% endhint %}

### Editor limits

Controls placement range and the nearby-sign picker when opening `/signs`.

* `Config.editorMaxDistance` — Metres the sign proxy can be moved from the player during placement. Prevents placing signs across the entire map in one session.
* `Config.nearbyDistance` — Metres searched for existing signs when `/signs` runs. Signs in range appear in the edit picker; increase if admins struggle to find signs in large lots.

**Example:** Allow placement further from the admin camera in open areas:

```lua
Config.editorMaxDistance = 200.0
Config.nearbyDistance = 75.0
```

### Layout and creator sliders

Default spacing and the min/max/step values for sliders in the sign creator. Server-side clamps apply on save — clients cannot bypass these ranges.

* `Config.lineGap` — Default vertical gap between lines (font units × sign scale). Used for new signs and as the fallback when loading old rows.
* `Config.panelPadding` — Extra space around text when auto-sizing the background panel (`x` horizontal, `y` vertical, in font units).
* `Config.panelDepth` — How far the panel sits behind the glyphs along the sign's forward axis.
* `Config.panelSizeRange` — Width/height multipliers on the auto-sized panel (`1.0` = fit text + padding). `default` is the starting slider value.

**Example:** Tighter default line spacing for stacked menu boards:

```lua
Config.lineGap = 0.9
```

### Database

`ls_signs` requires **oxmysql** — ensure it is installed and started before `ls_signs`. The `ls_signs` table is created automatically on first boot; no manual SQL import is required.

## Locale

Player-facing strings for keybinds and similar UI labels are in `locale.lua`. See [Locale | Translations](./locale-or-translations.md).

## After changing config

1. Save `config.lua` and/or `server/editables.lua`.
2. Run `refresh` then `ensure ls_signs` (or restart the server).
3. Reconnect or re-run `/signs` if admin status changed.
4. NUI rebuild is **not** required for config or locale changes unless you edited files under `web/` source.
