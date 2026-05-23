# Configuration (config.lua)

All server-side tuning for `ls_mining` lives in `config.lua` at the resource root. The mining shop catalog is in `shop/items.lua`. NPC market behavior constants are in `server/editables/economy.lua`.

After any Lua config change, restart the resource:

```cfg
refresh
ensure ls_mining
```

If you changed NUI strings in `locale.lua` or UI assets under `html/src/`, rebuild the NUI first:

```bash
cd html && npm run build
```

Then restart the resource.

## config.lua (full file)

Complete default config as shipped. Edit this file in your resource folder.

```lua
Config = {}

--- Floating mining phone UI (stats, shop, leaderboards). Third-party phone apps use a separate embed path.
Config.mining_phone = {
    --- Chat command to open/close the UI (e.g. /miningPhone, /miningPhone leaderboards/)
    command = 'miningPhone',
    --- When true, registers a FiveM keybind; players can rebind it in Settings → Key Bindings → FiveM
    register_keybind = true,
    --- Default key when register_keybind is true (e.g. 'F7', 'F6', 'm')
    default_keybind = 'J',
}

--- Client-only layout zone labels inside cave interiors (see CONTEXT.md: Config debug mode).
Config.debug = false

--- Global blocker defaults (per-zone overrides: blocker_xp, dynamite_needed)
Config.blocker = {
    xp = 50,
    dynamite_needed = 1,
    interaction_distance = 20.0,
    model = 'ls_blocker',
    z_spawn_offset = -1.0,
    --- Blast knockback (see CONTEXT.md: Blast knockback)
    blast_knockback_radius = 50.0,
    blast_knockback_force = 20.0,
    blast_knockback_ragdoll_ms = 2000,
    blast_knockback_lift = 0.2,
    blast_broadcast_radius = 50.0,
    blast_shake_radius = 25.0,
    --- Positional blast audio via invisible native explosion (see blocker_blast.lua)
    blast_sound = {
        enabled = true, -- set false if anticheat flags AddExplosion native
        explosion_type = 2, -- EXPLOSION_GRENADE
    },
}

--- When false, caves never auto-reset (blockers stay cleared, zones stay unlocked).t
--- Per-cave override: set `reset.enabled = false` on a cave entry.
Config.cave_reset_enabled = true

--- Defaults for layout zones not listed in Config.caves (e.g. open_zone)
Config.cave_zone_defaults = {
    max_rocks = 100,
    --- Legacy field; pickaxe mining uses shop pickaxe `damage_per_hit` instead.
    damage_per_hit = 8,
    exp_per_hit = {
        chance = 100,
        exp = 15,
    },
    presets = {
        gold = 50,
        copper = 50,
    },
    respawn_time = { min = 10 * 1000, max = 300 * 1000 },
}

Config.cave_blips = {
    blips_enabled = true,
    blip = {
        sprite = 618,
        color = 5,
        scale = 0.9,
        label = 'blip.mine',
    },
}

--- Each cave gets a map blip at `cave_entrance.coords` (outside hatch).
--- Defaults come from `Config.cave_blips` above; per-cave fields override only what you set:
---
---   blips_enabled — omit to inherit `Config.cave_blips.blips_enabled`; set false to hide
---                   this cave's blip, or true to show it when the global default is false
---   blip          — shallow merge with `Config.cave_blips.blip` (sprite, color, scale, label)
---
--- Example (custom label, inherit sprite/color/scale from defaults):
---   blip = { label = 'blip.mine' },
---
--- Inside exit props + enter spawn, relative to the cave shell anchor (`coords` / `model`).
--- Per-cave `cave_exit` shallow-merges with these defaults (omit a field to inherit).
Config.cave_exit_defaults = {
    shaft = {
        model = 'm23_2_prop_m32_liftshaft_01a',
        coords = vector3(36.856, 48.418, -5.865),
    },
    hatch = {
        model = 'ch_prop_ch_hatch_liftshaft_01a',
        coords = vector3(36.87, 48.41, -2.7),
    },
    player = vector3(36.87, 45.0, -2.7),
}

Config.caves = {
    {
        id = 'medium_mine_main',
        model = 'ls_mine_01',
        coords = vector3(1198.34, 4077.35, 262.04),
        rotation = vector3(0, 0, 0),
        cave_entrance = {
            coords = vector3(329.82,2870.29, 42.5),
            rotation = vector3(0, 0, 25),
        },
        --- Inside "Exit mine" props (offsets from `coords`; ls_mine_01 layout)
        cave_exit = {
            shaft = {
                coords = vector3(63.27, 37.15, -7),
            },
            hatch = {
                coords = vector3(63.27, 37.15, -3.8),
            },
            player = vector3(61.27, 35.15, -2.5),
        },
        reset = {
            hours = 24,
        },
        zones = {
            open_zone = {
                max_rocks = 100,
                respawn_time = { min = 10 * 1000, max = 300 * 1000 },
                damage_per_hit = 8,
                exp_per_hit = {
                    chance = 100,
                    exp = 15,
                },
                presets = {
                    gold = 50,
                    copper = 50,
                },
            },
            zone_1 = {
                dynamite_needed = 15,
                max_rocks = math.random(3, 8),
                respawn_time = { min = 10 * 1000, max = 300 * 1000 },
                damage_per_hit = math.random(4, 10),
                exp_per_hit = {
                    chance = 100,
                    exp = math.random(10, 20)
                },
                presets = {
                    gold = 0,
                    copper = 100
                }
            },
        },
    },
    {
        id = 'big_mine_main',
        model = 'ls_mine_02',
        coords = vector3(2940.57, 2785.01, 800.0),
        --- Heading of the cave prop anchor (same basis as layout offsets / GetOffsetFromEntityInWorldCoords)
        rotation = vector3(0, 0, 15),
        cave_entrance = {
            coords = vector3(2942.670, 2744.328, 42.271),
            rotation = vector3(0, 0, 195)
        },
        --- Inside "Exit mine" props (offsets from `coords`; ls_mine_02 layout)
        cave_exit = {
            shaft = {
                coords = vector3(36.856, 48.418, -5.865),
            },
            hatch = {
                coords = vector3(36.87, 48.41, -2.7),
            },
            player = vector3(36.87, 45.0, -2.7),
        },
        --- Per-cave scheduled reset. Set `enabled = false` to disable for this cave only.
        --- Interval (first matching unit wins): hours, days, or weeks
        reset = {
            hours = 24,
        },
        zones = {
            open_zone = {
                max_rocks = 100,
                respawn_time = { min = 10 * 1000, max = 300 * 1000 },
                damage_per_hit = 8,
                exp_per_hit = {
                    chance = 100,
                    exp = 15,
                },
                presets = {
                    gold = 50,
                    copper = 50,
                },
            },
            zone_1 = {
                dynamite_needed = 5,
                max_rocks = math.random(3, 8),
                respawn_time = { min = 10 * 1000, max = 300 * 1000 },
                damage_per_hit = math.random(4, 10),
                exp_per_hit = {
                    chance = 100,
                    exp = math.random(10, 20)
                },
                presets = {
                    gold = 0,
                    copper = 100
                }
            },
            zone_2 = {
                dynamite_needed = 7,
                max_rocks = 15,
                respawn_time = { min = 10 * 1000, max = 300 * 1000 },
                damage_per_hit = math.random(4, 10),
                exp_per_hit = {
                    chance = 100,
                    exp = math.random(10, 20)
                },
                presets = {
                    gold = 50,
                    copper = 50
                }
            },
            zone_3 = {
                dynamite_needed = 10,
                max_rocks = 15,
                respawn_time = { min = 10 * 1000, max = 300 * 1000 },
                damage_per_hit = math.random(4, 10),
                exp_per_hit = {
                    chance = 100,
                    exp = math.random(10, 20)
                },
                presets = {
                    gold = 50,
                    copper = 50
                }
            },
            zone_4 = {
                dynamite_needed = 1,
                max_rocks = 15,
                respawn_time = { min = 10 * 1000, max = 300 * 1000 },
                damage_per_hit = math.random(4, 10),
                exp_per_hit = {
                    chance = 100,
                    exp = math.random(10, 20)
                },
                presets = {
                    gold = 50,
                    copper = 50
                }
            },
            zone_5 = {
                dynamite_needed = 1,
                max_rocks = 15,
                respawn_time = { min = 10 * 1000, max = 300 * 1000 },
                damage_per_hit = math.random(4, 10),
                exp_per_hit = {
                    chance = 100,
                    exp = math.random(10, 20)
                },
                presets = {
                    copper = 100
                }
            },
        }
    }
}

--- Rank XP thresholds. Tuned so King of The Hill ≈ 25h of tracked mining time
--- (ls_mining_stats.time adds 2s per successful pickaxe hit).
Config.experience = {
    ['Rock Scraper'] = 0,
    ['Gravel Rat'] = 5000,
    ['Ore Seeker'] = 25000,
    ['Stone Destroyer'] = 750000,
    ['Prospector'] = 210000,
    ['Core Miner'] = 315000,
    ['Crystal Harvester'] = 490000,
    ['King of The Hill'] = 700000,
}

-- Rank-based perk definitions (single source of truth for gameplay + NUI)
-- Keys MUST match Config.experience rank names.
-- `perks`   = display strings shown in NUI
-- `unlocks` = boolean feature gates (sticky-true forward through ranks)
-- `bonuses` = additive numeric values aggregated up to current rank
Config.rank_perks = {
    ['Rock Scraper'] = {
        perks = {},
        unlocks = {
            blasting = false,
        },
        bonuses = {},
    },
    ['Gravel Rat'] = {
        perks = {
            'rank.perk.gravel_rat.blasting',
        },
        unlocks = {
            blasting = true,
        },
        bonuses = {
            xp_bonus_pct = 2,
        },
    },
    ['Ore Seeker'] = {
        perks = {
            'rank.perk.ore_seeker.yield_rarity',
        },
        bonuses = {
            yield_bonus_pct = 5,
            rarity_shift_pct = 3,
        },
    },
    ['Stone Destroyer'] = {
        perks = {
            'rank.perk.stone_destroyer.xp_smelt',
        },
        bonuses = {
            xp_bonus_pct = 5,
            smelting_efficiency_pct = 5,
        },
    },
    ['Prospector'] = {
        perks = {
            'rank.perk.prospector.rarity',
        },
        bonuses = {
            rarity_shift_pct = 5,
        },
    },
    ['Core Miner'] = {
        perks = {
            'rank.perk.core_miner.yield_bar',
        },
        bonuses = {
            yield_bonus_pct = 5,
            smelting_bonus_bar_chance = 5,
        },
    },
    ['Crystal Harvester'] = {
        perks = {
            'rank.perk.crystal_harvester.rarity_smelt',
        },
        bonuses = {
            rarity_shift_pct = 7,
            smelting_efficiency_pct = 5,
        },
    },
    ['King of The Hill'] = {
        perks = {
            'rank.perk.king_of_the_hill.master',
        },
        bonuses = {
            yield_bonus_pct = 5,
            xp_bonus_pct = 5,
            smelting_bonus_bar_chance = 5,
        },
    },
}

Config.smelting = {
    ls_iron_ore = {
        label = 'ore.iron',
        count = 2,                   -- amount of ores needed for 1 bar
        ore_model = 'ls_iron', -- props you will see in on the tray in smelting miningame
        bar_item = 'ls_iron_bar',    -- inventory item you will receive after collecting bar
        bar_texture_variation = 15,  -- texture varianation to change bar prop color. Here's an image of all available bar colors: https://cdn.lith.store/u/bar_colors.png
    },
    ls_copper_ore = {
        label = 'ore.copper',
        count = 2,
        ore_model = 'ls_copper_ore',
        bar_texture_variation = 15,
        bar_item = 'ls_copper_bar',
    },
    ls_silver_ore = {
        label = 'ore.silver',
        count = 3,
        ore_model = 'ls_silver_ore',
        bar_model = 'ls_ingot',
        bar_texture_variation = 8,
        bar_item = 'ls_silver_bar',
    },
    ls_gold_ore = {
        label = 'ore.gold',
        count = 2,
        ore_model = 'ls_gold_ore',
        bar_model = 'ls_ingot',
        bar_texture_variation = 15,
        bar_item = 'ls_gold_bar',
    }
}

Config.items = {
    ls_iron_bar = {
        min_price = 50,
        max_price = 200
    },
    ls_copper_bar = {
        min_price = 300,
        max_price = 3000
    },
    ls_silver_bar = {
        min_price = 500,
        max_price = 5000
    },
    ls_gold_bar = {
        min_price = 800,
        max_price = 8000
    },
    -- Sold as is no need to smelt it
    ls_diamond = {
        min_price = 5000,
        max_price = 10000
    }
}

--
--- Rock preset loot is granted once on destruction (**Rock destruction payout**).
--- Item counts below are ~5× the former per-hit baseline to preserve ore/hour after removing `drop_chance`.
Config.rock_presets = {
    gold = {
        model = 'ls_copper',
        health = 100,
        item_chances = {
            common = 80,  --%
            rare = 17,    --%
            legendary = 3 --%
        },
        items = {
            common = {
                rock = math.random(5, 10),
                ls_silver_ore = math.random(5, 10)
            },
            rare = {
                goldore = math.random(5, 10),
            },
            legendary = {
                diamond = math.random(5, 10)
            }
        }
    },
    copper = {
        model = 'ls_iron_ore',
        health = 100,
        item_chances = {
            common = 80,  --%
            rare = 17,    --%
            legendary = 3 --%
        },
        items = {
            common = {
                rock = math.random(5, 10),
                ls_silver_ore = math.random(5, 10)
            },
            rare = {
                goldore = math.random(5, 10),
            },
            legendary = {
                diamond = math.random(5, 10)
            }
        }
    }
}

Config.shop_crate = {
    coords = vector3(2829.51, 2806.89, 57.39),
    blips_enabled = true,
    blip = {
        sprite = 478,
        color = 2,
        scale = 0.8,
        label = 'blip.mining_shop',
    },
}

Config.npc_sales = {
    default_model = 's_m_m_strvend_01',
    blips_enabled = true,
    blip = {
        sprite = 52,
        color = 2,
        scale = 0.8,
        label = 'blip.ore_buyer',
    },
}

Config.smelting_tables = {
    blips_enabled = true,
    blip = {
        sprite = 436,
        color = 47,
        scale = 0.8,
        label = 'blip.smelting_table',
    },
}

Config.pickaxe_item_ids = {
    'ls_pickaxe_rusty',
    'ls_pickaxe_gold',
    'ls_pickaxe_iron',
    'ls_pickaxe_diamond',
}

--- When false, pickaxe durability is not read or written; equip/mining use slot item-name checks only.
Config.pickaxe_durability_enabled = true

Config.pickaxe_bonus_caps = {
    yield_bonus_pct = 40,
    rarity_shift_pct = 35,
}
```

## shop/items.lua (full file)

Mining shop catalog, pickaxe tiers, and dynamite fuse timing. Helper functions below `Shop.items` in the source file are runtime code — edit only the `Shop` table unless you know what you are changing.

```lua
Shop = {}

Shop.enabled = true

--- Ms between dynamite plant anim and explosion (cave blockers).
Shop.fuse_delay = 5000

-- Items available for purchase in the mining shop.
-- `id`    = unique string key sent from NUI to server
-- `type`  = 'pickaxe' or 'consumable'
-- `level` = minimum rank index (1-based, matches Config.experience sorted order)
-- `price` = money cost deducted via kq_link
-- `item`  = inventory item granted on purchase (nil = no item, perk-only)
-- `count` = amount of items granted (default 1)
-- `prop`  = GTA V prop model name (pickaxe equip visual, dynamite plant prop)
-- `dynamite` = true for inventory items usable on cave blockers (optional)
--
-- Pickaxe-only fields:
--   `damage_per_hit`         = health removed per successful pickaxe hit
--   `yield_bonus_pct`        = additive yield bonus on rock destruction payout
--   `rarity_shift_pct`       = additive rarity shift on rock destruction payout
--   `wear_chance_pct`        = % chance each successful hit procs durability loss
--   `wear_loss_min`          = minimum durability lost when wear procs
--   `wear_loss_max`          = maximum durability lost when wear procs
Shop.items = {
    {
        id = 'ls_pickaxe_rusty',
        type = 'pickaxe',
        level = 1,
        label = 'shop.item.rusty_pickaxe',
        price = 50,
        item = 'ls_pickaxe_rusty',
        count = 1,
        prop = 'ls_pickaxe_rusty',
        damage_per_hit = 8,
        yield_bonus_pct = 0,
        rarity_shift_pct = 0,
        wear_chance_pct = 40,
        wear_loss_min = 2,
        wear_loss_max = 4,
    },
    {
        id = 'ls_pickaxe_iron',
        type = 'pickaxe',
        level = 2,
        label = 'shop.item.iron_pickaxe',
        price = 250,
        item = 'ls_pickaxe_iron',
        count = 1,
        prop = 'ls_pickaxe_iron',
        damage_per_hit = 10,
        yield_bonus_pct = 2,
        rarity_shift_pct = 1,
        wear_chance_pct = 30,
        wear_loss_min = 1,
        wear_loss_max = 3,
    },
    {
        id = 'ls_pickaxe_gold',
        type = 'pickaxe',
        level = 3,
        label = 'shop.item.gold_pickaxe',
        price = 150,
        item = 'ls_pickaxe_gold',
        count = 1,
        prop = 'ls_pickaxe_gold',
        damage_per_hit = 12,
        yield_bonus_pct = 5,
        rarity_shift_pct = 3,
        wear_chance_pct = 20,
        wear_loss_min = 1,
        wear_loss_max = 2,
    },
    {
        id = 'ls_pickaxe_diamond',
        type = 'pickaxe',
        level = 4,
        label = 'shop.item.diamond_pickaxe',
        price = 250,
        item = 'ls_pickaxe_diamond',
        count = 1,
        prop = 'ls_pickaxe_diamond',
        damage_per_hit = 16,
        yield_bonus_pct = 8,
        rarity_shift_pct = 6,
        wear_chance_pct = 10,
        wear_loss_min = 1,
        wear_loss_max = 2,
    },
    {
        id = 'ls_miner_hat',
        type = 'consumable',
        level = 3,
        label = 'shop.item.miner_hat',
        price = 250,
        item = 'ls_miner_hat',
        count = 1,
        prop = 'ls_miner_hat',
        yield_bonus_pct = 7,
        rarity_shift_pct = 5,
    },
    {
        id = 'ls_dynamite_stick',
        type = 'consumable',
        level = 4,
        label = 'shop.item.dynamite_stick',
        price = 1500,
        item = 'ls_dynamite',
        count = 1,
        prop = 'ch_prop_ch_explosive_01a',
        dynamite = true,
    },
    {
        id = 'ls_dynamite_pack',
        type = 'consumable',
        level = 4,
        label = 'shop.item.dynamite_pack',
        price = 2500,
        item = 'ls_dynamite',
        count = 3,
        prop = 'ch_prop_ch_explosive_01a',
        dynamite = true,
    },
}
```

## server/editables/economy.lua (full file)

Demand-based NPC ore-buyer market tuning. Price bounds for each item come from `Config.items` above.

```lua
--- Economy tuning settings for demand-based NPC sale pricing.
--- All market behavior constants live here so server owners can adjust
--- without touching core logic.

EconomySettings = {}

EconomySettings.update_interval_ms = 15 * 60 * 1000 -- 15 minutes between price recalculations

EconomySettings.demand_response = 0.08 -- fraction of price range moved per "full pressure" window

EconomySettings.recovery_rate = 0.03 -- fraction of distance-to-midpoint recovered each window with zero demand

-- Per-player anti-manipulation: max effective units one player can contribute
-- to demand pressure per item per update window.
EconomySettings.player_window_cap = 20

-- Quick-sell quantity presets shown in the NUI.
EconomySettings.sell_presets = { 1, 5, 10 } -- "all" is always appended by the UI
```

## Tuning guide

Section-by-section notes for the most commonly changed values.

### General

* `Config.debug` — client-only **layout zone debug labels** inside caves. Leave `false` on production.
* `Config.mining_phone` — stats phone command and optional keybind.
* `Config.cave_reset_enabled` — global cave reset toggle; per-cave `reset.enabled = false` overrides one cave.

### Framework and integration

`ls_mining` supports **ESX**, **QBCore**, and **Qbox** via **kq_link**. There is no local `Config.framework` — configure your framework in kq_link.

{% hint style="warning" %}
Do not add a local `Config.framework` block — it is not used. All character IDs and names resolve via kq_link exports.
{% endhint %}

### Caves and layout zones

* `Config.caves` — each entry is one **cave interior** with surface hatch, optional reset schedule, and per-zone tuning.
* Zone keys (`open_zone`, `zone_1`, …) must match `shared/cave_layouts/`.
* `max_rocks` — target rock population; `respawn_time` in **milliseconds**.
* `presets` — weighted **rock preset** keys for spawned mineable rocks.
* `dynamite_needed` — sticks to clear the zone **cave blocker** (omit on `open_zone`).
* `Config.cave_zone_defaults` — fallback for zones not listed under a cave entry.
* `Config.cave_exit_defaults` — inside exit props; per-cave `cave_exit` shallow-merges.

{% hint style="info" %}
Zone `damage_per_hit` is legacy. **Pickaxe damage** comes from `shop/items.lua` only. Zone `exp_per_hit` still grants XP per successful hit.
{% endhint %}

### Cave blockers

* `Config.blocker.xp` — XP when a blocker is fully cleared.
* `Config.blocker.blast_knockback_*` — ragdoll push for nearby players (no HP damage).
* `Config.blocker.blast_sound.enabled` — set `false` if anticheat flags `AddExplosion`.

### Map blips

* `Config.cave_blips` — **cave map blip** defaults at surface hatches; per-cave overrides shallow-merge.
* `Config.shop_crate` — bootstrap **shop crate location** (seeds DB if empty).
* `Config.npc_sales` / `Config.smelting_tables` — blip defaults for DB-placed peds and smelting tables.
* All `blip.label` values are **locale keys** (see [Locale](./locale-or-translations.md)).

### Rank progression

* `Config.experience` — total XP thresholds; rank names must match `Config.rank_perks` keys.
* `Config.rank_perks` — locale perk lines, boolean unlocks (sticky forward), and additive bonuses.
* Tracked mining time: `ls_mining_stats.time` adds **2 seconds per successful pickaxe hit**. Max rank ≈ 25 h at default thresholds.

### Rock loot, smelting, economy

* `Config.rock_presets` — **rock destruction payout** on zero health (one roll per rock).
* `Config.smelting` — ore-to-bar recipes and smelting minigame props.
* `Config.items` — NPC sell price bounds; live prices use `EconomySettings`.

### Pickaxes and shop

* `Config.pickaxe_item_ids` — items treated as pickaxes.
* `Config.pickaxe_durability_enabled` — toggle full durability subsystem.
* `Config.pickaxe_bonus_caps` — max stacked yield/rarity bonus.
* `Shop.items` — pickaxe damage, wear rates, rank gates, and prices. Every pickaxe row needs complete `wear_*` fields.

## Locale

User-facing strings live in `locale.lua`. Config fields like `blip.mine` and shop `label` keys resolve through `L()` at runtime. See [Locale | Translations](./locale-or-translations.md).

## After changing config

| Change type | Action |
|-------------|--------|
| `config.lua`, `shop/items.lua`, server Lua | `ensure ls_mining` |
| `locale.lua` or `html/src/**` | `cd html && npm run build`, then restart |
| New inventory items | Register in your framework **and** match names in config/shop |
| SQL schema | Run migration SQL manually; no auto-migrate |

## Related pages

* [Overview](./README.md) — features and installation
* [Locale | Translations](./locale-or-translations.md)
