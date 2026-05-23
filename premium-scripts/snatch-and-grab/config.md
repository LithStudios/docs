# Config

```lua
Config = {}

Config.debug = false

--DEBUG FUNCTION! Teleports player to victim ped in the zone
Config.go_to_victim_ped = false

Config.zone_distance = 80.0 -- victim's spawn radius

-- Chance for the victim to spawn when player enters an available zone
Config.ped_spawn_chance = 100 -- percentage

Config.allow_looting_dead_peds = true

-- How long will NPCs not spawn in the area
-- Cooldowns on area are triggered when a certain number of NPCS spawn in area
-- This number can be adjusted per area in Config.areas
Config.area_cooldown = 30 -- in seconds

Config.display_victim_radius = false -- whether to show player the radius of the victim

--- Amount of correct key presses for player to complete snatching minigame
Config.keyCount = {
    min = 3,
    max = 5
}

-- Controls whether the script can only start if there are enough police players online
Config.police_check = {
    enabled = true,
    jobs = {
        'police',
        'sheriff',
        'state',
    },
    min_amount = 2, -- Minimum number of police players required online to start snatching
}

Config.dispatch = {
    --The chance that dispatch will be notified after crime commited
    alert_chance = 50, -- percentage
    --Jobs that will get notified
    jobs = {
        'police',
        'sherriff'
    },

    blip = {
        sprite = 408,
        color = 1,
        scale = 1.5,
        text = "Smash 'n grab",
        flash = true
    }
}

-- Get the list of controls here: https://docs.fivem.net/docs/game-references/controls/
Config.inputs = {
    snatch = {
        key = 'E',
        control = '~INPUT_CONTEXT~'
    },
    drop = {
        key = 'X',
        control = '~INPUT_VEH_DUCK~'
    },
    loot = {
        key = 'E',
        control = '~INPUT_CONTEXT~'
    }
}

Config.victim_ped_models = {'A_F_Y_Vinewood_01', 'U_F_Y_COMJane', 'G_F_Y_Vagos_01', 'G_F_Y_Families_01',
                            'A_M_Y_Business_01', 'A_M_M_Business_01', 'A_M_Y_Business_03', 'A_M_Y_Business_02'}

Config.loot = {
    --How many different items bag can hold
    --Items can duplicate! E.g Can give two cash items with different amounts
    amount = {
        min = 1,
        max = 5
    },

    --Determines the amount that the item will give
    --First table value determines minimum amount and second value - maximum amount
    items = {
        ['phone'] = {1,5},
        ['money'] = {1,5},
        ['mastercard'] = {1,5},
        ['clothing'] = {1,5},
    },

    props = {
        xm_prop_x17_ld_case_01 = {
            offset = vector3(0.1, 0, 0),
            rotation = vector3(90, 275, 0),
            ped_bone = 0xDEAD
        },
        prop_security_case_01 = {
            offset = vector3(0.11, 0, -0.02),
            rotation = vector3(90, 275, 0),
            ped_bone = 0xDEAD
        },
        prop_box_guncase_01a = {
            offset = vector3(0.23, -0.02, -0.01),
            rotation = vector3(195, 0, 70),
            ped_bone = 0xDEAD
        },
        hei_p_attache_case_shut = {
            offset = vector3(0.11, -0.02, -0.04),
            rotation = vector3(195, 0, 70),
            ped_bone = 0xDEAD
        },
        hei_prop_heist_thermite_case = {
            offset = vector3(0.25, -0.01, -0.05),
            rotation = vector3(195, 185, 85),
            ped_bone = 0xDEAD
        },
        w_am_case = {
            offset = vector3(0.01, 0.01, -0.02),
            rotation = vector3(100, 185, 90),
            ped_bone = 0xDEAD
        },
        vw_prop_casino_shopping_bag_01a = {
            offset = vector3(0.27, -0.02, -0.05),
            rotation = vector3(10, 275, 350),
            ped_bone = 0xDEAD
        }
    }
}

-- ped_limit is how many NPCS can spawn in the same zone
-- count_until_cooldown is how many times an NPC needs to spawn in the area to trigger area cooldown
Config.areas = {
    {coords = vector3(-586.43, -959.61, 22.01), ped_limit = 1, count_until_cooldown = 1},
    {coords = vector3(-1031.29, -1651.25, 3.99), ped_limit = 1, count_until_cooldown = 1},
    {coords = vector3(-1146.57, -1496.12, 3.75), ped_limit = 1, count_until_cooldown = 1},
    {coords = vector3(-1227.72, -1372.41, 3.71), ped_limit = 1, count_until_cooldown = 1},
    {coords = vector3(-1408.82, -912.28, 10.61), ped_limit = 1, count_until_cooldown = 1},
    {coords = vector3(-1227.47, -781.67, 17.50), ped_limit = 1, count_until_cooldown = 1},
    {coords = vector3(-1311.01, -656.42, 25.87), ped_limit = 1, count_until_cooldown = 1},
    {coords = vector3(-1470.31, -230.05, 49.23), ped_limit = 1, count_until_cooldown = 1},
    {coords = vector3(-977.16, -220.01, 37.39), ped_limit = 1, count_until_cooldown = 1},
    {coords = vector3(-476.15, -326.23, 41.55), ped_limit = 1, count_until_cooldown = 1},
    {coords = vector3(123.01, -24.87, 67.27), ped_limit = 1, count_until_cooldown = 1},
    {coords = vector3(-44.93, 31.35, 71.38), ped_limit = 1, count_until_cooldown = 1},
    {coords = vector3(-391.02, 123.67, 64.91), ped_limit = 1, count_until_cooldown = 1},
    {coords = vector3(-3.43, -135.03, 56.56), ped_limit = 1, count_until_cooldown = 1},
    {coords = vector3(820.65, -183.34, 72.35), ped_limit = 1, count_until_cooldown = 1},
    {coords = vector3(1204.67, -376.28, 68.43), ped_limit = 1, count_until_cooldown = 1},
    {coords = vector3(973.87, -664.22, 56.66), ped_limit = 1, count_until_cooldown = 1},
    {coords = vector3(1196.18, -769.45, 57.48), ped_limit = 1, count_until_cooldown = 1},
    {coords = vector3(921.86, -2250.61, 29.89), ped_limit = 1, count_until_cooldown = 1},
    {coords = vector3(945.05, -1886.96, 30.53), ped_limit = 1, count_until_cooldown = 1},
    {coords = vector3(515.79, -1896.54, 25.17), ped_limit = 1, count_until_cooldown = 1},
    {coords = vector3(95.99, -1869.22, 23.42), ped_limit = 1, count_until_cooldown = 1},
    {coords = vector3(-66.01, -1717.07, 29.05), ped_limit = 1, count_until_cooldown = 1},
    {coords = vector3(239.07, -1724.54, 28.49), ped_limit = 1, count_until_cooldown = 1},
    {coords = vector3(81.41, -1357.05, 28.62), ped_limit = 1, count_until_cooldown = 1},
    {coords = vector3(-270.51, -1424.50, 30.57), ped_limit = 1, count_until_cooldown = 1},
    {coords = vector3(1853.60, 3723.60, 32.42), ped_limit = 1, count_until_cooldown = 1},
    {coords = vector3(1872.31, 3900.99, 32.71), ped_limit = 1, count_until_cooldown = 1},
    {coords = vector3(1609.39, 3672.94, 34.11), ped_limit = 1, count_until_cooldown = 1},
    {coords = vector3(1399.13, 3584.14, 34.74), ped_limit = 1, count_until_cooldown = 1},
    {coords = vector3(1695.26, 4649.05, 43.24), ped_limit = 1, count_until_cooldown = 1},
    {coords = vector3(1668.24, 4848.83, 41.65), ped_limit = 1, count_until_cooldown = 1},
    {coords = vector3(-111.78, 6420.44, 30.49), ped_limit = 1, count_until_cooldown = 1},
    {coords = vector3(-298.24, 6228.97, 31.07), ped_limit = 1, count_until_cooldown = 1},
    {coords = vector3(-3026.84, 598.63, 7.25), ped_limit = 1, count_until_cooldown = 1},
    {coords = vector3(-2975.71, 434.65, 17.81), ped_limit = 1, count_until_cooldown = 1},
    {coords = vector3(-3143.53, 1076.88, 20.24), ped_limit = 1, count_until_cooldown = 1},
    {coords = vector3(202.75, -841.89, 30.66), ped_limit = 1, count_until_cooldown = 1},
    {coords = vector3(-181.54, -891.79, 29.33), ped_limit = 1, count_until_cooldown = 1},
    {coords = vector3(1202.37, -3232.56, 5.98), ped_limit = 1, count_until_cooldown = 1},
    {coords = vector3(-914.35, -2207.76, 6.08), ped_limit = 1, count_until_cooldown = 1},
    {coords = vector3(13.56, -555.18, 36.93), ped_limit = 1, count_until_cooldown = 1},
    {coords = vector3(210.88, 196.43, 105.60), ped_limit = 1, count_until_cooldown = 1},
    {coords = vector3(210.88, 196.43, 105.60), ped_limit = 1, count_until_cooldown = 1},
    {coords = vector3(-1057.84, -1926.09, 13.10), ped_limit = 1, count_until_cooldown = 1},
    {coords = vector3(-1082.89, -1041.02, 2.08), ped_limit = 1, count_until_cooldown = 1},
    {coords = vector3(-959.96, -1092.37, 2.15), ped_limit = 1, count_until_cooldown = 1},
    {coords = vector3(345.19, -1136.71, 29.27), ped_limit = 1, count_until_cooldown = 1},
    {coords = vector3(2575.65, 420.32, 108.45), ped_limit = 1, count_until_cooldown = 1},
    {coords = vector3(508.10, 79.81, 96.39), ped_limit = 1, count_until_cooldown = 1}
}




```
