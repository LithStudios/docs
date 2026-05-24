---
description: >-
  Full underground mining gameplay — cave interiors, pickaxe mining, dynamite
  blasting, smelting, ranks, shop, and an in-game stats phone.
---

# Mining & Smelting

## Overview

`ls_mining` adds a full mining loop to your FiveM server — underground caves, pickaxe mining, smelting, ranks, and an in-game stats phone. Players can:

* Enter **cave interiors** via surface hatches and mine **mineable rocks** with a pickaxe minigame
* Clear **cave blockers** with dynamite to unlock deeper layout zones (requires the blasting rank unlock)
* Smelt ore into bars at admin-placed **smelting tables**
* Sell bars and gems to ore-buyer NPCs (demand-based pricing)
* Buy pickaxes, dynamite, and gear from the **stats phone** shop; collect purchases from **shop crates**
* Track XP, ranks, perks, and leaderboards in the **stats phone** (`/miningPhone` by default)

Supports **ESX**, **QBCore**, and **Qbox** via [kq_link](https://github.com/Kuzkay/kq_link). Framework selection is configured in kq_link, not in `ls_mining`.

Main files:

* `config.lua` — caves, ranks, loot, blips, smelting recipes ([Configuration](./config.md))
* `shop/items.lua` — mining shop catalog, pickaxe tiers, dynamite fuse timing
* `locale.lua` — all player-facing strings ([Locale | Translations](./locale-or-translations.md))
* `sql/init.sql` — database tables (run once before first start)
* `server/editables/economy.lua` — NPC ore-buyer market tuning
* `client/` / `server/` — gameplay, persistence, NUI bridge

## Installation

{% stepper %}
{% step %}

### Place the resource

Put the `ls_mining` folder in your server resources directory (e.g. `/resources/[lith]/ls_mining/`).
{% endstep %}

{% step %}

### Install dependencies

* [kq_link](https://github.com/Kuzkay/kq_link) — inventory, economy, entity interactions, player identity
* `ls_mining_props` — cave shells, rocks, smelting props (declared in `fxmanifest.lua`)
* MySQL — `oxmysql` or `mysql-async` (auto-detected at runtime)

Register inventory items used by the script (pickaxes, ores, bars, dynamite). Item names must match `shop/items.lua`, `Config.smelting`, and `Config.rock_presets`.
{% endstep %}

{% step %}

### Import the database

Run `sql/init.sql` once on your server database. This creates experience, stats, smelting tables, cave progress, shop pending delivery, interior props, and NPC market tables.

{% hint style="warning" %}
The resource does not auto-migrate schema. Apply any future `.sql` files manually when updating.
{% endhint %}
{% endstep %}

{% step %}

### Add admin permissions

Add one of the following to `server.cfg` so admins can place smelting tables, ore buyer NPCs, and shop crates:

```cfg
add_ace group.admin ls_mining.admin allow
```

Or grant permission to a specific license:

```cfg
add_ace fivem:XXXXXX ls_mining.admin allow
```

Replace `XXXXXX` with the admin's FiveM license identifier.
{% endstep %}

{% step %}

### Ensure in server.cfg

```cfg
ensure oxmysql
ensure kq_link
ensure ls_mining_props
ensure ls_mining
```

Start `kq_link` and `ls_mining_props` before `ls_mining`.
{% endstep %}

{% step %}

### Restart the server

After changing `server.cfg`, **restart your entire server** for ACE permissions and `ensure` lines to take effect. `refresh` + `ensure` alone does not reload `server.cfg`.

Then verify:

* Check the console for dependency errors (missing kq_link exports, SQL, props)
* Enter a configured cave hatch and test pickaxe mining on a dev server first
{% endstep %}

{% step %}

### Place world features

In-game, admins with `ls_mining.admin` can run `/place` to set up:

* **Smelting tables** — where players smelt ore into bars
* **Ore buyer NPCs** — where players sell bars and gems
* **Shop crate locations** — where shop purchases spawn for pickup

Switch modes in the placement UI, confirm each location where you want it, and delete or reset entries as needed. Positions are saved to MySQL and sync to all players.
{% endstep %}
{% endstepper %}

{% hint style="warning" %}
Hard dependencies: **kq_link**, **ls_mining_props**, and a working MySQL connection. If kq_link is missing or misconfigured, inventory payouts, shop purchases, and entity prompts will not work.
{% endhint %}

## Configuration

All primary tuning is in `config.lua`. Shop items and pickaxe stats live in `shop/items.lua`. See [Configuration (config.lua)](./config.md) for section-by-section guidance.

## Admin setup

Some world features are placed at runtime and stored in MySQL (not hardcoded in `config.lua`):

| Feature | Storage | Notes |
|---------|---------|-------|
| Smelting tables | `ls_mining_smelting_tables` | Requires `ls_mining.admin` ACE |
| Ore buyer NPCs | `ls_mining_npc_sales` | Requires `ls_mining.admin` ACE |
| Shop crate locations | `ls_mining_shop_crate` | Bootstraps from `Config.shop_crate` if empty |
| Interior props | `ls_mining_interior_props` | Edited in-cave with `/mineinterior` |

Grant `ls_mining.admin` during [installation](#installation), then use `/place` for smelting tables, ore buyers, and shop crates.

## Gameplay flow

{% stepper %}
{% step %}

### Equip and enter

Players buy a pickaxe from the stats phone shop, equip it, and travel to a **cave map blip** (surface hatch). Interact to run the hatch enter sequence into the **cave interior**.
{% endstep %}

{% step %}

### Mine rocks

With an **equipped pickaxe**, interact with a **mineable rock** to open the pickaxe minigame. Successful hits reduce rock health; when health reaches zero, the **rock finisher** receives the **rock destruction payout** (ore loot) and XP. Partial mining grants XP only — no ore until the rock is destroyed.
{% endstep %}

{% step %}

### Clear blockers

From **Gravel Rat** rank onward, players with dynamite can place sticks on **cave blockers** to unlock the next **layout zone**. Each zone may require multiple sticks (`dynamite_needed`). Nearby players receive **blast knockback** (no HP damage).
{% endstep %}

{% step %}

### Smelt and sell

At a **smelting table**, players choose ore and run the smelting minigame to produce bars. Ore buyers (NPCs) purchase bars and gems; prices move with server demand (see `server/editables/economy.lua`).
{% endstep %}

{% step %}

### Progress ranks

Mining XP accumulates on the **player experience record**. Ranks unlock perks (yield, rarity, smelting bonuses) and the blasting gate. Open the stats phone to view progress, leaderboards, and the shop.
{% endstep %}
{% endstepper %}

## Stats phone

Players open the floating UI with the command set in `Config.mining_phone.command` (default `/miningPhone`). Optional keybind defaults to `J` when `register_keybind = true`.

Example routes:

* `/miningPhone` — Mining stats tab
* `/miningPhone smelting/` — Smelting stats tab
* `/miningPhone leaderboards/` — Leaderboards
* `/miningPhone shop/` — Mining shop

## Troubleshooting

### Resource not starting

* Confirm `ensure ls_mining` and dependencies in `server.cfg`
* Verify kq_link exports exist (`AddPlayerItemToFit`, `GetPlayerCharacterId`, etc.)
* Check that `ls_mining_props` is started

### Database errors

* Confirm `sql/init.sql` was imported
* Ensure oxmysql or mysql-async is running and connected

### No rocks or floating props in caves

* Confirm `ls_mining_props` models are streaming
* Cave shell anchor must match `Config.caves` coords — misaligned caves break layout rock placement

### Anticheat flags explosions

Set `Config.blocker.blast_sound.enabled = false` if your anticheat blocks the native explosion used for blocker blast audio.

## Related pages

* [Configuration (config.lua)](./config.md)
* [Locale | Translations](./locale-or-translations.md)
* [Getting started](https://docs.lith.store/information/getting-started) — shared Lith install checklist
