---
description: >-
  Includes an in-game NUI editor, client-side visual/audio/drunk-style layers,
  overdose handling, and server-side persistence.
icon: capsule
---

# Drug Effects Creator

### Features

* **Drug creator/editor (NUI)**: create / edit / rename / delete drugs and their effect timelines.
* **Effect layers**: camera shake, timecycle, NUI visuals + sounds, walk/clipsets, ragdoll, spawned peds/animals/objects, events, player boosts, input effects.
* **Overdose system**: risk accumulation + configurable warning/overdose timelines (stored in DB).
* **Persistence**: saves drugs to DB and can **resume active effects** after reconnect (per player).
* **Framework support**: `esx`, `qb`, `qbox` (set in `config.lua`).
* **Admin gating**: ACE permission (`ls_drugs.admin`) and/or identifier allowlist (`server/admin.lua`).<br>

### Installation

1. **Copy resource**
   * Place this folder in your server resources, e.g. `resources/[lith]/ls_drugs`.
2. **Database**
   * Import `ls_drugs.sql` into your server database.
   * (Optional) Import presets from `presets/*.sql`.
3. **Dependencies**
   * Ensure the dependencies listed below are installed and started **before** `ls_drugs`.
4. **Configure**
   * Edit `config.lua` and set `Config.framework` to `esx`, `qb`, or `qbox`.
5. **Permissions**
   * Grant ACE permission for admins (Pick one):
     * `add_ace group.admin ls_drugs.admin allow`
     * `add_ace fivem:XXXXXX ls_drugs.admin allow`
   * Or add identifiers in `server/admin.lua`.
6. **Start the resource**
   * Add to `server.cfg`:
     * `ensure ls_drugs`

### Dependencies

* **MySQL driver**: `oxmysql` (default; configurable via `ls_drugs_sql_driver`)
* **Inventory/item bridge**: [`kq_link`](https://github.com/Kuzkay/kq_link) (used to register usable items and remove items on use)
* **Framework (one of)**:
  * `es_extended` (ESX)
  * `qb-core` (QB)
  * `qbx_core` (Qbox)<br>

### Drug Items

Each drug needs a matching item in your inventory system. The item name is either:

* The key used in the drug config (e.g. `ls_shrooms`)
* Or a custom `itemName` field set on the drug in the in-game editor

Add items to your inventory items file (e.g. `qb-core/shared/items.lua` or `ox_inventory/data/items.lua` items):

**QB-Core example:**

```lua
['ls_shrooms'] = {name = 'ls_shrooms', label = 'Shrooms', weight = 100, type = 'item', image = 'ls_shrooms.png', unique = false, useable = true, shouldClose = true, combinable = nil, description = 'Magic mushrooms'},
```

**ox\_inventory example** (`data/items.lua`):

```lua
['ls_shrooms'] = {
    label = 'Shrooms',
    weight = 100,
    stack = true,
    close = true,
},
```

***

### Preset Drugs (Optional)

Two preset SQL files are included in `presets/`:

* `presets/generic_drugs.sql` - generic drug set
* `presets/kq_drugs.sql` - Imports presets for [KuzQuality](https://kuzquality.com/) drug items

Import one (or both) to pre-populate drug configurations:

***

### Performance notes

* **Most cost comes from visuals** (spawned objects/peds/animals, heavy timecycle/camera effects). Keep timelines and spawn rates reasonable.
* **Tune prop density** via `Config.visual_prop_range` in `config.lua`.
* **DB load is light** (drugs load on resource start; active effects are upserted per use and cleaned up on resume).
* If you allow many concurrent users with long/complex timelines, prefer fewer concurrent entity-spawning layers and shorter durations.

### Where to get it

* Get it here: [https://lith.store/package/drug-effects-creator](https://lith.store/package/drug-effects-creator)
