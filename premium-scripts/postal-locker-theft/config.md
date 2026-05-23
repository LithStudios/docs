---
description: Configuration file for postal locker theft.
---

# Config

```lua
-- MAKE SURE THE KQ_LINK IS INSTALLED AND RUNNING BEFORE THIS SCRIPT
-- GET KQ_LINK FOR FREE HERE: https://github.com/Kuzkay/kq_link

Config = {}

Config.debug = false

Config.lockers = {
    {
        coords = vector3(47.676, 99.946, 77.903),
        rotation = vector3(0.3, -0.8, 68.9),
        size = 2, -- 1 for small, 2 for large
        model = 2 -- 1 for PostOp, 2 for GoPostal
    },
    {
        coords = vector3(302.455, -908.788, 28.297),
        rotation = vector3(0, 0, 160),
        size = 1,
        model = 1
    },
    {
        coords = vector3(58.614, -1734.654, 28.2),
        rotation = vector3(0, 0, -130),
        size = 1,
        model = 1
    },
    {
        coords = vector3(307.477, -1456.315, 28.974),
        rotation = vector3(0, 0, -130),
        size = 2,
        model = 2
    },
    {
        coords = vector3(-134.854, -672.818, 34),
        rotation = vector3(0.6, -1.7, 70.7),
        size = 2,
        model = 1
    },
    {
        coords = vector3(-102.691, 40.295, 70.43),
        rotation = vector3(0, 0, -115),
        size = 1,
        model = 2
    },
    {
        coords = vector3(-1354.168, -668.830, 24.75),
        rotation = vector3(1, 1, -60),
        size = 1,
        model = 2
    },
    {
        coords = vector3(1959.083, 3737.763, 31.377),
        rotation = vector3(0, 0, -61),
        size = 1,
        model = 1
    },
    {
        coords = vector3(535.066, -151.285, 56.031),
        rotation = vector3(0, 0, -177),
        size = 1,
        model = 1
    },
    {
        coords = vector3(1150.808, -291.685, 67.975),
        rotation = vector3(0, 0, -170),
        size = 2,
        model = 1
    },
    {
        coords = vector3(73.980, -1563.551, 28.562),
        rotation = vector3(0, 0, -130),
        size = 2,
        model = 2
    },
    {
        coords = vector3(-168.340, -150.667, 42.736),
        rotation = vector3(0, 0, -19),
        size = 2,
        model = 2
    },
}

--Time it takes to loot props
Config.loot_times = {
    small = 2,  -- seconds
    medium = 3, -- seconds
    large = 5   -- seconds
}

Config.inputs = {
    drop = {
        key = 'X',
        control = '~INPUT_VEH_DUCK~'
    },
    loot = {
        key = 'E',
        control = '~INPUT_CONTEXT~'
    },
    hack = {
        key = 'F',
        control = '~INPUT_VEH_DUCK~'
    },
    pick_up = {
        key = 'E',
        control = '~INPUT_CONTEXT~'
    },
    break_in = {
        key = 'L',
        control = '~INPUT_CONTEXT~'
    }
}

Config.props = {
    ['small'] = {
        'prop_drug_package_02',
        'm23_2_prop_m32_package_01a',
        'v_ret_ps_box_03',
        'v_ret_ps_box_01',
        'prop_cs_box_clothes',
        'prop_box_guncase_02a'
    },
    ['medium'] = {
        'v_ret_gc_ammo5',
        'v_ret_gc_ammo3',
        'hei_prop_heist_deposit_box',
        'ba_prop_battle_antique_box',
        'prop_box_ammo07a',
        'm23_1_prop_m31_box_metal_01a',
        'sf_prop_sf_box_cigar_01a',

    },
    --If you add more props here, you will also have to add a key-value pair in Config.prop_attach
    ['large'] = {
        'v_res_filebox01',
        'v_serv_abox_04',
        'prop_paper_box_05',
        'hei_prop_heist_box',
        'prop_cs_cardbox_01'
    }
}

Config.prop_attach = {
    ['v_res_filebox01'] = {
        offset = vector3(0.08, 0.12, -0.27),
        rotation = vector3(166, 69, -257),
        ped_bone = 0xDEAD
    },
    ['v_serv_abox_04'] = {
        offset = vector3(0.02, 0.12, -0.28),
        rotation = vector3(69, 0, 30),
        ped_bone = 0xDEAD
    },
    ['prop_paper_box_05'] = {
        offset = vector3(0.02, 0.12, -0.28),
        rotation = vector3(69, 0, 30),
        ped_bone = 0xDEAD
    },
    ['hei_prop_heist_box'] = {
        offset = vector3(0.02, 0.12, -0.28),
        rotation = vector3(69, 0, 30),
        ped_bone = 0xDEAD
    },
    ['prop_cs_cardbox_01'] = {
        offset = vector3(0.02, 0.12, -0.28),
        rotation = vector3(69, 0, 30),
        ped_bone = 0xDEAD
    }
}

--How long until looted locker can reset
Config.locker_reset_cooldown = {
    value = 10,
    units = 'minutes' -- 'minutes' or 'seconds'
}

Config.loot = {
    --The chance that the cell will be empty
    empty_cell_chance = 10, -- percentage

    --Chance that the loot will be empty
    empty_loot_chance = 20, -- percentage

    --Amount of items that a player can receive from 1 loot item
    amounts = {
        small = {
            min = 1,
            max = 2
        },
        medium = {
            min = 2,
            max = 3
        },
        large = {
            min = 4,
            max = 6
        }
    },

    --Determines the amount that the item will give
    --First table value determines minimum amount and second value - maximum amount
    items = {
        small = {
            ['phone'] = { 1, 5 },
            ['money'] = { 1, 5 },
            ['mastercard'] = { 1, 5 },
            ['clothing'] = { 1, 5 },
        },
        medium = {
            ['phone'] = { 1, 5 },
            ['money'] = { 1, 5 },
            ['mastercard'] = { 1, 5 },
            ['clothing'] = { 1, 5 },
        },
        large = {
            ['phone'] = { 1, 5 },
            ['money'] = { 1, 5 },
            ['mastercard'] = { 1, 5 },
            ['clothing'] = { 1, 5 },
        }
    },
}

-- Hacking minigame configuration
Config.hack = {
    code_length = 4,   -- Length of the code to guess (4 digits by default)
    max_attempts = 8,  -- Maximum number of attempts allowed
    timer_length = 90, -- Time limit in seconds
}

-- Sequence minigame configuration
Config.sequence = {
    min = 1, -- minimum amount of keys
    max = 6 -- maximum amount of keys
}

Config.particles = {
    enable = true,
    particle_asset = 'core',
    particle_name = 'ent_anim_dusty_hands',
    particle_scale = 2.0,
    particle_play_length = 2000
}

Config.dispatch = {
    enabled = true,
    jobs = { 'police', 'bsco', 'lspd' }, -- player with either of these jobs will get the alert
    blip = {
        sprite = 4,
        color = 1,
        scale = 1.5,
        text = L('dispatch_blip_message'),
        flash = false
    }
}
```
