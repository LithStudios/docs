---
description: Configuration file for wheelspacers
---

# Config

```lua
--- FOLLOW installationGuide.md BEFORE STARTING SCRIPT!!!

Config = {}

Config.framework = 'esx' -- esx or qbcore

Config.useNewESXExport = true

Config.debug = false

-- Name of jack stand item
Config.jackStand = 'ls_jackstand'

-- 'mysql', 'oxmysql', others might work as well
Config.sqlDriver = 'mysql'

Config.identifier = "license"-- OPTIONS: license, xbl, live, discord, fivem, license2

Config.target = {
    enabled = true,
    system = 'ox_target' -- 'qtarget' or 'qb-target' or 'ox_target'  (Other systems might work as well)
}

-- If wheel spacers can only be mounted by players with a certain job
-- You can add several jobs
Config.job = {
    jobOnly = true,
    names = {
        'mechanic',
        ''
    }
}

Config.wheelProp = 'prop_wheel_01'

--Client's render distance for modified "spaced" cars
Config.renderRadius = 100.0

--- ONLY ENABLE IF YOU KNOW WHAT YOU ARE DOING
Config.enableCustomJackAnimations = false

Config.animations = {
    -- animation which plays when player is unmounting a wheel
    ['unmounting'] = {
        dict = 'amb@prop_human_movie_bulb@idle_a',
        anim = 'idle_b',

        dictZ = 'anim@amb@clubhouse@tutorial@bkr_tut_ig3@', -- animation that will play if the wheel is higher than player
        animZ = 'machinic_loop_mechandplayer'
    },

    -- animation which plays when player is mounting a wheel
    ['mounting'] = {
        dict = 'amb@prop_human_movie_bulb@idle_a',
        anim = 'idle_b',

        dictZ = 'anim@amb@clubhouse@tutorial@bkr_tut_ig3@', -- animation that will play if the wheel is higher than player
        animZ = 'machinic_loop_mechandplayer'
    },

    -- animation which plays when player is installing a spacer
    ['spacerInstall'] = {
        dict = 'amb@prop_human_movie_bulb@idle_a',
        anim = 'idle_b',

        dictZ = 'anim@amb@clubhouse@tutorial@bkr_tut_ig3@', -- animation that will play if the spacer is higher than player
        animZ = 'machinic_loop_mechandplayer'
    },

    -- animation which plays when player is uninstalling a spacer
    ['spacerRemove'] = {
        dict = 'amb@prop_human_movie_bulb@idle_a',
        anim = 'idle_b',

        dictZ = 'anim@amb@clubhouse@tutorial@bkr_tut_ig3@', -- animation that will play if the spacer is higher than player
        animZ = 'machinic_loop_mechandplayer'
    }
}

Config.keybinds = {
    unMountWheel = {
       label = 'E',
    },
    mountWheel = {
        label = 'E',
    },
    mountSpacer = {
        label = 'E',
    },
    unMountSpacer = {
        label = 'E',
    },
    pickUpWheel = {
        label = 'E',
    },
    lowerVehicle = {
        label = 'X',
    },
    stopBoltMinigame = {
        label = 'X',
        name = 'INPUT_VEH_DUCK'
    },
    dropWheel = {
        label = 'X',
        name = 'INPUT_VEH_DUCK'
    },
    putSpacerBackInInventory = {
        label = 'X',
        name = 'INPUT_VEH_DUCK'
    }
}

Config.shop = {
    accountName = 'bank', -- account that will get charged
    useShop = true, -- if player can buy items from shop
    jobOnly = false, -- if shop is only accessible to player who have the job

    -- coords for spacers and jackstand
    items = {
        {
            label = '10mm spacer',
            model = 'wheel_spacer_red',
            name = 'ls_spacer_red',
            x = -213.3,
            y = -1337.4,
            z = 34.3,
            price = 150
        },
        {
            label = '15mm spacer',
            model = 'wheel_spacer_black',
            name = 'ls_spacer_black',
            x = -213.3,
            y = -1337.0,
            z = 34.3,
            price = 175
        },
        {
            label = '20mm spacer',
            model = 'wheel_spacer_hardened',
            name = 'ls_spacer_hardened',
            x = -213.3,
            y = -1336.6,
            z = 34.3,
            price = 200
        },
        {
            label = '30mm spacer',
            model = 'wheel_spacer_silver',
            name = 'ls_spacer_silver',
            x = -213.3,
            y = -1336.2,
            z = 34.3,
            price = 225
        },
        {
            label = '40mm spacer',
            model = 'wheel_spacer_gold',
            name = 'ls_spacer_gold',
            x = -213.3,
            y = -1335.8,
            z = 34.3,
            price = 250
        },
        {
            label = 'Jack Stand',
            model = 'imp_prop_axel_stand_01a',
            name = 'ls_jackstand',
            x = -213.8,
            y = -1336.1,
            z = 34.3,
            price = 1000,
            isJack = true
        }

    }
}


--- CHANGE X AND Y VALUES TO CONTROL CAMBER
--- The higher the X value, the more the wheel will stick out of the vehicle
--- The higher the Y value, the more the wheel will tilt out of the vehicle
Config.spacers = {
    ['10 mm'] = {
        x = 0.1 / 2,
        y = 0.1 / 3,
        model = 'wheel_spacer_red',
        name = 'ls_spacer_red'
    },
    ['15 mm'] = {
        x = 0.15 / 2,
        y = 0.15 / 3,
        model = 'wheel_spacer_black',
        name = 'ls_spacer_black'
    },
    ['20 mm'] = {
        x = 0.2 / 2,
        y = 0.2 / 3,
        model = 'wheel_spacer_hardened',
        name = 'ls_spacer_hardened'
    },
    ['30 mm'] = {
        x = 0.3 / 2,
        y = 0.3 / 3,
        model = 'wheel_spacer_silver',
        name = 'ls_spacer_silver'
    },
    ['40 mm'] = {
        x = 0.4 / 2,
        y = 0.4 / 3,
        model = 'wheel_spacer_gold',
        name = 'ls_spacer_gold'
    }
}

```
