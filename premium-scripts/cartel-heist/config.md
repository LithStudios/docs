---
description: Configuration file for Cartel Island Heist
---

# Config

```lua

Config                          =   {}                                                      
Config.debug                    =   false

-- Whether NPCs shoot at players.
Config.npcShoot                 =   true

-- Let players loot if only all items can be carried. (Except bags)
Config.canPlayerCarryAll        =   false

-- Render distance for the island.
Config.renderDistance           =   500.0

-- Model for boats.
Config.boatModel                =   'dinghy2'

-- Model for helicopter.
Config.helicopterModel          =   'buzzard'

-- Whether to output island reset logs to the server console.
Config.getConsoleOutput         =   false

-- Time interval for island reset in milliseconds.
Config.islandResetTime          =   3600000

-- Time interval for items reset in milliseconds.
Config.itemsResetTime           =   900000

-- Delay time for island reset if someone is on the island or in an interior in milliseconds.
Config.resetTimeDelay           =   60000

-- Cooldown time for interacting with interior enter/exit in milliseconds.
Config.interiorCooldown         =   2000



Config.target = {
    enabled = true,
    system = 'ox_target'    -- 'qtarget' or 'qb-target'  (Other systems might work as well)
}

--- SETTINGS FOR ESX
Config.esxSettings = {
    enabled = true,    
    useNewESXExport = true,
    account = 'money',
    oldEsx = false,
}

--- SETTINGS FOR QBCORE
Config.qbSettings = {
    enabled = false,
    UseNewQBExport = true,  -- Make sure to uncomment the old export inside fxmanifest.lua if you're still using it
    account = 'cash',
}

Config.alternativeIdentifier = {
    enabled = true,
    identifier = "discord"  -- OPTIONS: license, xbl, live, discord, fivem, license2
}

Config.sqlDriver = "mysql"

Config.interiorExitCoords = { x = -213.86, y = 6291.14, z = -39.16}


---------------------------------------------------
---                 Buyer options               
---------------------------------------------------

-- Define properties for the blip representing the buyer.
Config.buyer = {
    blip = {
        enabled = true,     -- Whether the blip is enabled or not.
        sprite  = 207,      -- Sprite ID for the blip on the map.
        color   = 81,       -- Color of the blip.
        alpha   = 255,      -- Transparency level of the blip.
        scale   = 1.0       -- Scale of the blip.
    },
    
    ped         = true,    -- Whether the ped is enabled or not.
    
    marker      = false,   -- Whether the marker is enabled or not.
    
    -- Define the location of the buyer.
    location = {
        x = 2525.48,        -- X-coordinate of the buyer's location.
        y = 4980.82,        -- Y-coordinate of the buyer's location.
        z = 44.85,          -- Z-coordinate of the buyer's location.
        heading = 57.77     -- Heading direction of the buyer.
    },
    
    -- Define color properties for the marker.
    ['MarkerColor'] = {
        r = 0,              -- Red component of the marker color.
        g = 100,            -- Green component of the marker color.
        b = 0,              -- Blue component of the marker color.
        a = 100             -- Alpha/transparency level of the marker color.
    }  
}

-- Configuration settings for drawing 3D text.

Config.Draw3dTextOptions = {
    fontId = 4,     -- ID of the font used for the 3D text.
    scaleX = 0.1,   -- Scale of the text on the X-axis.
    scaleY = 0.1    -- Scale of the text on the Y-axis.
}

-- Configuration settings for item prices.

-- The item prices are randomly generated within specified ranges using math.random.

Config.itemPrice = {
    ['ls_weed_block']   = math.random(250, 500),    -- Price range for weed blocks.
    ['ls_weed_bag']     = math.random(100, 250),    -- Price range for weed bags.
    ['ls_coke_block']   = math.random(1000, 2500),  -- Price range for cocaine blocks.
    ['ls_coke_powder']  = math.random(250, 500),    -- Price range for cocaine powder.
    ['ls_jewellery']    = math.random(1000, 1500)   -- Price range for jewellery.
}

-- Note: Instead of random prices, fixed constant prices could also be used.
-- For example:
-- Config.itemPrice = {
--     ['ls_weed_block']   = 350,    -- Fixed price for weed blocks.
--     ['ls_weed_bag']     = 150,    -- Fixed price for weed bags.
--     ['ls_coke_block']   = 2000,   -- Fixed price for cocaine blocks.
--     ['ls_coke_powder']  = 300,    -- Fixed price for cocaine powder.
--     ['ls_jewellery']    = 1200    -- Fixed price for jewellery.
-- }



-- Configuration settings for island coordinates.

Config.islandCoords = {
    hint = {
        enabled = true,     -- Whether the hint is enabled or not.
        color = 1,          -- Color of the hint.
        alpha = 128         -- Transparency level of the hint.
    },
    coords = {
        x = -1215.98,       -- X-coordinate of the island.
        y = 7100.97,        -- Y-coordinate of the island.
        z = -6.0,           -- Z-coordinate of the island.
        heading = 0.0       -- Heading direction of the island.
    }    
}

-- Configuration settings for entrance coordinates.

Config.entranceCoords = {
    coords = {
        x = 65.64,          -- X-coordinate of the entrance. (Offset from the island)
        y = 73.56,          -- Y-coordinate of the entrance. (Offset from the island)   
        z = 5.98            -- Z-coordinate of the entrance. (Offset from the island)
    }    
}

-- Configuration settings for keys.

-- Model for keys.
Config.key = {
    model                 =   'bkr_prop_jailer_keys_01a',
    blip = {
        enabled = true,     -- Whether the blip is enabled or not.
        sprite  = 71,       -- Sprite ID for the blip on the map.
        color   = 30,       -- Color of the blip.
        alpha   = 255,      -- Transparency level of the blip.
        scale   = 1.0,      -- Scale of the blip.
        time    = 60000,       -- Time in milliseconds (ms) after which the blip appears after the key spawns.
    }
}

-- Configuration settings for wire cutters.

Config.wireCutters = {    
    blip = {
        enabled = true,     -- Whether the blip is enabled or not.
        sprite  = 71,       -- Sprite ID for the blip on the map.
        color   = 30,       -- Color of the blip.
        alpha   = 255,      -- Transparency level of the blip.
        scale   = 1.0       -- Scale of the blip.
    },
    locations = {
        {
            coords = {
                x = -533.08,    -- X-coordinate of the wire cutter location.
                y = 5292.81,    -- Y-coordinate of the wire cutter location.
                z = 74.23,      -- Z-coordinate of the wire cutter location.
                xRot = 0.0,     -- X-rotation of the wire cutter.
                yRot = 0.0,     -- Y-rotation of the wire cutter.
                zRot = 180.0    -- Z-rotation of the wire cutter.
            }
        },
        -- Additional locations can be added here.
    }
}

-- Configuration settings for allowed melee weapons to open crates (to open crates faster).

Config.meleeWeapon = {
    allowed = {
        'weapon_hatchet',       
        'weapon_battleaxe',     
        'weapon_crowbar'        
    }
}


Config.cartelNPCModels = {
    'A_M_M_EastSA_01',
    'CSB_Ramp_mex',
    'IG_Hao',
    'IG_Hao_02',
    'IG_Ortega',
    'S_M_Y_Robber_01',
}


Config.thermite = {
    blip = {
        enabled = true,             -- Whether the blip is enabled or not.
        sprite  = 486,              -- Sprite ID for the blip on the map.
        color   = 30,               -- Color of the blip.
        alpha   = 255,              -- Transparency level of the blip.
        scale   = 1.0               -- Scale of the blip.
    },
    model = 'hei_prop_heist_thermite',    -- Model of the thermite item.
    thermite = {
        offset = {
            x = 0.0,                 
            y = -0.075,              
            z = 0.0,                 
            h = 0.0,                 
        },
        rotation = {
            x = 90.0,                
            y = 90.0,                
            z = 0.0,                 
        },
    },
    locations = {
        {
            coords = {
                x = 2352.90,         
                y = 3137.67,         
                z = 48.52,           
                xRot = -0.00,        
                yRot = 0.00,         
                zRot = 180.00        
            }
        },
        {
            coords = {
                x = 2356.49,         
                y = 3136.78,         
                z = 47.24,           
                xRot = 0.00,         
                yRot = 0.00,         
                zRot = -8.00         
            }
        }
    }
}


-- Configuration settings for cartel island NPCs (on-foot).

-- Warning: Coordinates supposed to be declared with offset from the island (by using command /getcoords)

Config.cartelIslandNPC = {
    coords = {
        {
            x = 0.96, y = 7.28, z = 6.12, heading = 250.65
        },
        {
            x = -83.44, y = -79.04, z = 7.13, heading = 147.53
        },
        {
            x = -84.18, y = -47.73, z = 6.65, heading = 61.15
        },
        {
            x = -81.57, y = -32.25, z = 6.95, heading = 265.19
        },
        {
            x = -64.10, y = -23.39, z = 6.64, heading = 253.83
        },
        {
            x = -51.83, y = -21.32, z = 5.87, heading = 132.69
        },
        {
            x = -20.58, y = -4.31, z = 5.86, heading = 344.85
        },
        {
            x = -22.46, y = 17.31, z = 5.88, heading = 218.78
        },
        {
            x = -53.27, y = -74.15, z = 6.83, heading = 163.31
        },
        {
            x = -63.61, y = -41.77, z = 5.86, heading = 125.37
        },
        {
            x = -30.07, y = -38.64, z = 5.86, heading = 271.91
        },
        {
            x = -33.67, y = -21.63, z = 5.86, heading = 23.95
        },
        {
            x = -23.32, y = -19.03, z = 5.86, heading = 165.53
        },
        {
            x = -45.64, y = 9.20, z = 5.65, heading = 274.37
        },
        {
            x = -43.89, y = 14.46, z = 5.63, heading = 237.23
        },
        
    }
}

-- Configuration settings for cartel island backup NPCs (on-foot).
-- Warning: Coordinates supposed to be declared with offset from the island (by using command /getcoords)

Config.cartelBackupNPC = {
    coords = {
        {
            x = -60.26, y = -55.05, z = 5.86, heading = 315.49
        },
        {
            x = -39.21, y = -55.20, z = 6.21, heading = 299.09
        },
        {
            x = -29.70, y = -26.33, z = 5.86, heading = 309.45
        },
        {
            x = -80.05, y = 24.85, z = 4.44, heading = 61.54 
        },
        {
            x = -70.12, y = 25.07, z = 3.84, heading = 51.23
        },
        {
            x = -41.70, y = 14.39, z = 5.77, heading = 358.75
        },
        {
            x = -53.68, y = 0.30, z = 3.59, heading = 25.49
        },
        {
            x = -51.83, y = -21.32, z = 5.87, heading = 132.69
        },
           
        
    }
}


-- Configuration settings for EMP blocker.

-- The "goTo" variables x and y define the specific side of the item where the player will approach to pick it up.

Config.empBlocker = {
    blip = {
        enabled = true,             -- Whether the blip is enabled or not.
        sprite  = 544,              -- Sprite ID for the blip on the map.
        color   = 30,               -- Color of the blip.
        alpha   = 255,              -- Transparency level of the blip.
        scale   = 1.0               -- Scale of the blip.
    },
    amountToSpawn = 4,              -- Amount of EMP blockers to spawn.
    locations = {                   -- Locations where EMP blockers spawn (not commented as per request).
        {
            coords = {
                x = 2393.36, 
                y = 3065.14, 
                z = 51.09, 
                xRot = 3.24, 
                yRot = -15.03, 
                zRot = 180.0
            },
            goTo = {
                x = 0.6,
                y = 0.6
            }
        },
        {   
            coords = {
                x = 2381.17,
                y = 3095.90, 
                z = 47.19,
                xRot = -0.00, 
                yRot = 0.00, 
                zRot = -0.00
            },
            goTo = {
                x = 0.0,
                y = 0.6
            }
        },
        {
            coords = {
                x = 2348.15,
                y = 3140.30, 
                z = 48.53,
                xRot = -0.00, 
                yRot = 0.00, 
                zRot = -0.00
            },
            goTo = {
                x = 0.0,
                y = -0.6
            }
        },
        {
            coords = {
                x = 2142.93,
                y = 2905.00, 
                z = 49.81,
                xRot = -0.00, 
                yRot = 0.00, 
                zRot = 120.00
            },
            goTo = {
                x = -0.0,
                y = -0.6
            }
        },
        {
            coords = {
                x = 2075.39,
                y = 2950.92, 
                z = 46.34,
                xRot = 0.00, 
                yRot = 0.00, 
                zRot = -48.00
            },
            goTo = {
                x = 0.0,
                y = -0.6
            }
        },
        {
            coords = {
                x = 2050.73,
                y = 2946.82, 
                z = 56.57,
                xRot = -0.00, 
                yRot = -0.00, 
                zRot = -112.00
            },
            goTo = {
                x = 0.0,
                y = -0.6
            }
        },
    }
}








--  .d8888b.   .d88888b.  888b    888 88888888888        d8888 8888888 888b    888 8888888888 8888888b.   .d8888b.  
-- d88P  Y88b d88P" "Y88b 8888b   888     888           d88888   888   8888b   888 888        888   Y88b d88P  Y88b 
-- 888    888 888     888 88888b  888     888          d88P888   888   88888b  888 888        888    888 Y88b.      
-- 888        888     888 888Y88b 888     888         d88P 888   888   888Y88b 888 8888888    888   d88P  "Y888b.   
-- 888        888     888 888 Y88b888     888        d88P  888   888   888 Y88b888 888        8888888P"      "Y88b. 
-- 888    888 888     888 888  Y88888     888       d88P   888   888   888  Y88888 888        888 T88b         "888 
-- Y88b  d88P Y88b. .d88P 888   Y8888     888      d8888888888   888   888   Y8888 888        888  T88b  Y88b  d88P 
--  "Y8888P"   "Y88888P"  888    Y888     888     d88P     888 8888888 888    Y888 8888888888 888   T88b  "Y8888P"  
                                                                                                              
                                                                                                                 

Config.spots = {
    {
        pos = {             
            x = -1250.93,
            y = 7086.32,
            z = 7.15,
            h = 87.5,
        },
        container = 'small',
    },
    {
        pos = {
            x = -1192.64 ,
            y = 7154.152 ,
            z = 6.06,
            h = 75.48,
        },
        container = 'small',
    },   
    {   
        pos = {
            x = -217.16,
            y = 6271.42,
            z = -39.05,
            h = 216.10,
        },
        container = 'small',
    },   
}

Config.containers = {
    ['small'] = {
        main = {
            model = 'prop_container_04mb',
            offset = {
                x = 0.0,
                y = 0.0,
                z = -1.0,
                h = 270.0,
            },
        },
        lock = {
            model = 'hei_prop_container_lock',
            offset = {
                x = 0.0,
                y = -3.45,
                z = 1.25,
                h = 0.0,
            },
            rotation = {
                x = 0.0,
                y = 0.0,
                z = 0.0,
            },
        },
        doorLeft = {
            model = 'prop_container_door_mb_l',
            offset = {
                x = -1.295,
                y = -3.4,
                z = 1.4,
            },
            rotation = {
                x = 0.0,
                y = 0.0,
                z = 0.0,
            },
        },
        doorRight = {
            model = 'prop_container_door_mb_r',
            offset = {
                x = 1.295,
                y = -3.4,
                z = 1.4,
            },
            rotation = {
                x = 0.0,
                y = 0.0,
                z = 0.0,
            },
        },
        doorRearLeft = {
            model = 'prop_container_door_mb_l',
            offset = {
                x = 1.295,
                y = 3.4,
                z = 1.4,
            },
            rotation = {
                x = 0.0,
                y = 0.0,
                z = 180.0,
            },
        },
        doorRearRight = {
            model = 'prop_container_door_mb_r',
            offset = {
                x = -1.295,
                y = 3.4,
                z = 1.4,
            },
            rotation = {
                x = 0.0,
                y = 0.0,
                z = 180.0,
            },
        },
    }
}








--  .d8888b.  8888888b.         d8888 88888888888 8888888888  .d8888b.  
-- d88P  Y88b 888   Y88b       d88888     888     888        d88P  Y88b 
-- 888    888 888    888      d88P888     888     888        Y88b.      
-- 888        888   d88P     d88P 888     888     8888888     "Y888b.   
-- 888        8888888P"     d88P  888     888     888            "Y88b. 
-- 888    888 888 T88b     d88P   888     888     888              "888 
-- Y88b  d88P 888  T88b   d8888888888     888     888        Y88b  d88P 
--  "Y8888P"  888   T88b d88P     888     888     8888888888  "Y8888P"  


-- Configuration settings for crate spawn spots.

Config.cratesSpots = {
    {
        pos = {
            x = -223.50,
            y =  6269.71,
            z = -39.00,
            h =  1.09,
        },
        crate = 'single',
    },
    {
        pos = {
            x = -229.59,
            y =  6279.60,
            z = -39.0,
            h =  272.4,
        },
        crate = 'single',
    },
    {
        pos = {
            x = -215.58,
            y =  6277.99,
            z = -39.0,
            h =  80.4,
        },
        crate = 'single',
    }
}

Config.crates = {
    ['single'] = {
        main = {
            model = 'prop_ld_crate_01',
            offset = {
                x =  0.0,
                y =  0.0,
                z = -1.0,
                h =  270.0,
            },
        },
        top = {
            model = 'prop_ld_crate_lid_01',
            offset = {
                x = 0.0,
                y = 0.0,
                z = 0.56,
            },
            rotation = {
                x = 0.0,
                y = 0.0,
                z = 0.0,
            },
        }
    }
}


-- Configuration settings for different types of crates and their properties.

Config.crateTypes = {
    { 
        type = 'weed',      -- Type of the crate.
        props = {
            'weed_block1',  -- List of props associated with the weed crate type.
            'weed_block2',
            'weed_bag1',
            'weed_bag2',
            'weed_bag3',
            'weed_bag4',
            'weed_bag5',
            'weed_bag6',
        }
    },
    { 
        type = 'coke',      -- Type of the crate.
        props = {
            'coke_block1',  -- List of props associated with the coke crate type.
            'coke_block2',
            'coke_block3',
            'coke_block4',
            'coke_block5',
            'coke_block6',
            'coke_block7',
            'coke_block8', 
        }   
    },
    { 
        type = 'money',     -- Type of the crate.
        props = {
            'money_block1', -- List of props associated with the money crate type.
            'money_block2',
            'money_block3',
            'money_block4',
            'money_block5',
            'money_block6',
        }
    }
}



-- Configuration settings for crate opening animations and tools.

Config.crateOpening = {
    tool = {
        time = 1500,                                        -- Minimal value: 1500 milliseconds.
        dict = 'melee@large_wpn@streamed_core',             -- Animation dictionary for the tool.
        anim = 'plyr_front_takedown_bat_headhit'            -- Animation name for the tool.
    },
    unarmed = {
        time = 30000,                                       -- Time duration for opening without tools.
        dict = 'anim@amb@clubhouse@tutorial@bkr_tut_ig3@',  -- Animation dictionary for unarmed opening.
        anim = 'machinic_loop_mechandplayer'                -- Animation name for unarmed opening.
    }
}




-- 8888888b.  8888888b.   .d88888b.  8888888b.   .d8888b.  
-- 888  "Y88b 888   Y88b d88P" "Y88b 888   Y88b d88P  Y88b 
-- 888    888 888    888 888     888 888    888 Y88b.      
-- 888    888 888   d88P 888     888 888   d88P  "Y888b.   
-- 888    888 8888888P"  888     888 8888888P"      "Y88b. 
-- 888    888 888 T88b   888     888 888              "888 
-- 888  .d88P 888  T88b  Y88b. .d88P 888        Y88b  d88P 
-- 8888888P"  888   T88b  "Y88888P"  888         "Y8888P"  



Config.inside = {}
Config.inside.bigDrop = {
    'money_crate1',
    'money_crate2',
    'weed_pallete1',
    'weed_pallete2',
    'coke_stack2'
}

Config.inside.drop = {
    'weed_block1',
    'weed_block2',
    'weed_bag1',
    'weed_bag2',
    'weed_bag3',
    'weed_bag4',
    'weed_bag5',
    'weed_bag6',
    'coke_block1',
    'coke_block2',
    'coke_block3',
    'coke_block4',
    'coke_block5',
    'coke_block6',
    'coke_block7',
    'coke_block8',    
    'money_one1',
    'money_block1',
    'money_block2',
    'money_block3',
    'money_block4',
    'money_block5',
    'money_block6',
}



Config.inside.items = {
    ['weed_pallete1'] = {
        model = 'hei_prop_heist_weed_pallet',        
        reward = 'ls_weed_block',
        amount =  1
    },
    ['weed_pallete2'] = {
        model = 'hei_prop_heist_weed_pallet_02',
        reward = 'ls_weed_block',
        amount = 1
    },
    ['weed_block1'] = {
        model = 'prop_weed_block_01',
        reward = 'ls_weed_block',
        amount = 1
    },
    ['weed_block2'] = {
        model = 'hei_prop_heist_weed_block_01b',
        reward = 'ls_weed_block',
        amount = 1
    },
    ['weed_bag1'] = {
        model = 'bkr_prop_weed_smallbag_01a',
        reward = 'ls_weed_bag',
        amount = 1
    },
    ['weed_bag2'] = {
        model = 'bkr_prop_weed_bigbag_open_01a',
        reward = 'ls_weed_bag',
        amount = 1
    },
    ['weed_bag3'] = {
        model = 'bkr_prop_weed_bigbag_01a',
        reward = 'ls_weed_bag',
        amount = 1
    },
    ['weed_bag4'] = {
        model = 'bkr_prop_weed_bigbag_02a',
        reward = 'ls_weed_bag',
        amount = 1
    },
    ['weed_bag5'] = {
        model = 'bkr_prop_weed_bigbag_03a',
        reward = 'ls_weed_bag',
        amount = 1
    },
    ['weed_bag6'] = {
        model = 'ba_prop_battle_weed_bigbag_01a',
        reward = 'ls_weed_bag',
        amount = 1
    },
    ['money_one1'] = {
        model = 'bkr_prop_scrunched_moneypage',
        reward = 'ls_money_one',
        amount = 1
    },
    ['money_block1'] = {
        model = 'ba_prop_battle_moneypack_02a',
        reward = 'ls_money_medium',
        amount = math.random(500,2500)
    },
    ['money_block2'] = {
        model = 'bkr_prop_money_sorted_01',
        reward = 'ls_money_medium',
        amount = math.random(500,2500)
    },
    ['money_block3'] = {
        model = 'bkr_prop_money_unsorted_01',
        reward = 'ls_money_medium',
        amount = math.random(500,2500)
    },
    ['money_block4'] = {
        model = 'bkr_prop_money_wrapped_01',
        reward = 'ls_money_medium',
        amount = math.random(500,2500)
    },
    ['money_block5'] = {
        model = 'bkr_prop_moneypack_03a',
        reward = 'ls_money_medium',
        amount = math.random(500,2500)
    },
    ['money_block6'] = {
        model = 'h4_prop_h4_cash_bag_01a',
        reward = 'ls_money_medium',
        amount = math.random(500,2500)
    },
    ['money_crate1'] = {
        model = 'ex_prop_crate_money_bc',
        reward = 'ls_money_big',
        amount = math.random(2500, 7500)
    },
    ['money_crate2'] = {
        model = 'ex_prop_crate_money_sc',
        reward = 'ls_money_big',
        amount = math.random(2500, 7500)
    },
    ['coke_block1'] = {
        model = 'prop_coke_block_half_a',
        reward = 'ls_coke_block',
        amount = 1
    },
    ['coke_block2'] = {
        model = 'prop_coke_block_half_b',
        reward = 'ls_coke_block',
        amount = 1
    },
    ['coke_block3'] = {
        model = 'prop_coke_block_01',
        reward = 'ls_coke_block',
        amount = 1
    },
    ['coke_block4'] = {
        model = 'bkr_prop_coke_block_01a',
        reward = 'ls_coke_block',
        amount = 1
    },
    ['coke_block5'] = {
        model = 'bkr_prop_coke_cut_01',
        reward = 'ls_coke_block',
        amount = 1
    },
    ['coke_block6'] = {
        model = 'bkr_prop_coke_cut_02',
        reward = 'ls_coke_block',
        amount = 1
    },
    ['coke_block7'] = {
        model = 'ba_prop_battle_coke_block_01a',
        reward = 'ls_coke_block',
        amount = 1
    },    
    ['coke_block8'] = {
        model = 'bkr_prop_coke_cutblock_01',
        reward = 'ls_coke_block',
        amount = 1
    },
    ['coke_stack2'] = {
        model = 'h4_prop_h4_coke_stack_01a',
        reward = 'ls_coke_powder',
        amount = 1
    }
}



-- 8888888 888b    888 88888888888 8888888888 8888888b.  8888888  .d88888b.  8888888b.  
--   888   8888b   888     888     888        888   Y88b   888   d88P" "Y88b 888   Y88b 
--   888   88888b  888     888     888        888    888   888   888     888 888    888 
--   888   888Y88b 888     888     8888888    888   d88P   888   888     888 888   d88P 
--   888   888 Y88b888     888     888        8888888P"    888   888     888 8888888P"  
--   888   888  Y88888     888     888        888 T88b     888   888     888 888 T88b   
--   888   888   Y8888     888     888        888  T88b    888   Y88b. .d88P 888  T88b  
-- 8888888 888    Y888     888     8888888888 888   T88b 8888888  "Y88888P"  888   T88b 
                                                                                     
Config.doorOpeningSpeed =  0.2   -- Adjust door opening speed [0.1 - 1.0]  0.1 - slow ; 1.0 - fast

Config.cardCoords = {
    x = -219.956116, 
    y = 6292.504883, 
    z = -38.935513
}

-- Configuration settings for interior NPC positions within the cartel area.

-- NOTE: These coordinates are not offset of the interior/island, plain coordinates. 
-- You can get your current coordinates by using command /getc

Config.cartelInteriorNPC = {
    coords = {
        {
            x = -225.52, y = 6286.673, z = -39.16, heading = 250.60   -- Position and heading for NPC.
        },
        {
            x = -229.25, y = 6281.79, z = -39.04, heading = 267.01     -- Position and heading for NPC.
        },
        {
            x = -218.10, y = 6268.12, z = -39.12, heading = 39.79      -- Position and heading for NPC.
        },
        {
            x = -232.94, y = 6272.31, z = -38.69, heading = 266.92     -- Position and heading for NPC.
        },
        {
            x = -215.31, y = 6273.74, z = -39.17, heading = 31.06      -- Position and heading for NPC.
        },
    }
}


Config.tableItems = {
    ['single_ring1'] = {
        model = 'prop_jewel_03a',        
        reward = 'ls_jewellery',
        amount =  1
    },
    ['single_ring2'] = {
        model = 'prop_jewel_03b',        
        reward = 'ls_jewellery',
        amount =  1
    },
    ['multiple_rings'] = {
        model = 'prop_jewel_pickup_new_01',
        reward = 'ls_jewellery',
        amount = 1
    },
    ['single_watch1'] = {
        model = 'prop_jewel_02c',
        reward = 'ls_jewellery',
        amount = 1
    },
    ['single_watch2'] = {
        model = 'prop_jewel_02b',
        reward = 'ls_jewellery',
        amount = 1
    },
    ['single_watch3'] = {
        model = 'prop_jewel_02a',
        reward = 'ls_jewellery',
        amount = 1
    },
    ['multiple_watches'] = {
        model = 'ex_office_swag_jewelwatch',
        reward = 'ls_jewellery',
        amount = 1
    },
    ['single_skull'] = {
        model = 'p_jewel_pickup33_s',
        reward = 'ls_jewellery',
        amount = 1
    },
    ['single_necklace1'] = {
        model = 'p_jewel_necklace01_s',
        reward = 'ls_jewellery',
        amount = 1
    },
    ['single_necklace2'] = {
        model = 'p_jewel_necklace_02',
        reward = 'ls_jewellery',
        amount = 1
    },
    ['single_necklace3'] = {
        model = 'p_jewel_necklace02_s',
        reward = 'ls_jewellery',
        amount = 1
    },
    ['single_sapphire'] = {
        model = 'sf_prop_sf_jewel_01a',
        reward = 'ls_jewellery',
        amount = 1
    },
    ['multiple_bracelets1'] = {
        model = 'prop_jewel_04a',
        reward = 'ls_jewellery',
        amount = 1
    },
    ['multiple_bracelets2'] = {
        model = 'prop_jewel_04b',
        reward = 'ls_jewellery',
        amount = 1
    },
    ['multiple_bracelets3'] = {
        model = 'ex_office_swag_jewelwatch2',
        reward = 'ls_jewellery',
        amount = 1
    },
}

Config.tables = {
    coords = {
        {x = -245.8, y = 6268.65, z = -38.29, heading = 90.0},
        {x = -245.79, y = 6272.02, z = -38.29, heading = 0.0},
        {x = -243.28, y = 6272.01, z = -38.29, heading = 0.0},        
        {x = -241.07, y = 6268.88, z = -38.29, heading = 90.0}
    }
}

Config.tableDrop = {
    {
        props = {
            ['single_ring1'] = {
                x = 0.3,
                y = -0.4,
                z = 0.05,
                heading = 0.0
            },
            ['single_watch1'] = {
                x = 0.3,
                y = -0.6,
                z = 0.05,
                heading = 0.0
            },
            ['single_skull'] = {
                x = 0.2,
                y = 0.525,
                z = 0.07,
                heading = 0.0
            },
            ['single_necklace3'] = {
                x = 0.15,
                y = 0.6,
                z = 0.02,
                heading = 0.0
            },
            ['single_necklace2'] = {
                x = 0.15,
                y = 0.8,
                z = 0.02,
                heading = 0.0
            },
            ['multiple_bracelets1'] = {
                x = -0.15,
                y = -0.5,
                z = 0.05,
                heading = 0.0
            },
            ['multiple_rings'] = {
                x = -0.1,
                y = -0.2,
                z = 0.02,
                heading = 0.0
            },
            ['multiple_watches'] = {
                x = -0.3,
                y = 0.0,
                z = 0.00,
                heading = 0.0
            },
            ['single_ring2'] = {
                x = 0.3,
                y = 0.5,
                z = 0.00,
                heading = 0.0
            },            
        }
    },
    {
        props = {
            ['single_ring1'] = {
                x = -0.4,
                y = 0.0,
                z = 0.05,
                heading = 0.0
            },
            ['single_watch1'] = {
                x = -0.3,
                y = 0.0,
                z = 0.05,
                heading = 0.0
            },
            ['single_skull'] = {
                x = 0.525,
                y = -0.5,
                z = 0.07,
                heading = 0.0
            },
            ['single_necklace3'] = {
                x = 0.3,
                y = 0.05,
                z = 0.02,
                heading = 0.0
            },
            ['single_necklace2'] = {
                x = 0.5,
                y = 0.05,
                z = 0.02,
                heading = 0.0
            },
            ['multiple_bracelets1'] = {
                x = -0.5,
                y = -0.15,
                z = 0.05,
                heading = 0.0
            },
            ['multiple_rings'] = {
                x = -0.2,
                y = -0.1,
                z = 0.02,
                heading = 0.0
            },
            ['multiple_watches'] = {
                x = 0.0,
                y = -0.3,
                z = 0.00,
                heading = 0.0
            },
            ['single_ring2'] = {
                x = 0.5,
                y = 0.0,
                z = 0.00,
                heading = 0.0
            },            
        }
    },
    {
        props = {
            ['single_ring1'] = {
                x = -0.4,
                y = 0.0,
                z = 0.05,
                heading = 0.0
            },
            ['single_watch1'] = {
                x = -0.3,
                y = 0.0,
                z = 0.05,
                heading = 0.0
            },
            ['single_skull'] = {
                x = 0.525,
                y = -0.5,
                z = 0.07,
                heading = 0.0
            },
            ['single_necklace3'] = {
                x = 0.3,
                y = 0.05,
                z = 0.02,
                heading = 0.0
            },
            ['single_necklace2'] = {
                x = 0.5,
                y = 0.05,
                z = 0.02,
                heading = 0.0
            },
            ['multiple_bracelets1'] = {
                x = -0.5,
                y = -0.15,
                z = 0.05,
                heading = 0.0
            },
            ['multiple_rings'] = {
                x = -0.2,
                y = -0.1,
                z = 0.02,
                heading = 0.0
            },
            ['multiple_watches'] = {
                x = 0.0,
                y = -0.3,
                z = 0.00,
                heading = 0.0
            },
            ['single_ring2'] = {
                x = 0.5,
                y = 0.0,
                z = 0.00,
                heading = 0.0
            },            
        }
    },
    {
        props = {
            ['single_ring1'] = {
                x = 0.3,
                y = -0.4,
                z = 0.05,
                heading = 0.0
            },
            ['single_watch1'] = {
                x = 0.3,
                y = -0.6,
                z = 0.05,
                heading = 0.0
            },
            ['single_skull'] = {
                x = 0.2,
                y = 0.525,
                z = 0.07,
                heading = 0.0
            },
            ['single_necklace3'] = {
                x = 0.15,
                y = 0.6,
                z = 0.02,
                heading = 0.0
            },
            ['single_necklace2'] = {
                x = 0.15,
                y = 0.8,
                z = 0.02,
                heading = 0.0
            },
            ['multiple_bracelets1'] = {
                x = -0.15,
                y = -0.5,
                z = 0.05,
                heading = 0.0
            },
            ['multiple_rings'] = {
                x = -0.1,
                y = -0.2,
                z = 0.02,
                heading = 0.0
            },
            ['multiple_watches'] = {
                x = -0.3,
                y = 0.0,
                z = 0.00,
                heading = 0.0
            },
            ['single_ring2'] = {
                x = 0.3,
                y = 0.5,
                z = 0.00,
                heading = 0.0
            },            
        }
    }
    
}

Config.palletesBags = {
    prop = 'h4_prop_h4_big_bag_01a',


    coords = {
        {
            x = 0.5, 
            y = 0.00, 
            z = 0.425, 
            heading = 15.0
        },
        {
            x = -0.5, 
            y = 0.25, 
            z = 0.425, 
            heading = 30.0
        },
        {
            x = 0.0, 
            y = 0.00, 
            z = 0.425, 
            heading = -30.0
        }
    },
    drop = {
        'weed_block',
        'weed_bag',
        'coke_block', 
        'money',
    } 
}


Config.palleteItems = {
    ['weed_block'] = {
        reward = 'ls_weed_block',
        amount = 1
    },
    ['weed_bag'] = {
        reward = 'ls_weed_bag',
        amount = 1
    },
    ['money'] = {
        reward = 'ls_money_medium',
        amount = math.random(500,2500)
    },
    ['coke_block'] = {
        reward = 'ls_coke_block',
        amount = 1
    },
}


Config.policeJobNames = {
    'police'
}
------------------------------------------
--- DISPATCH
------------------------------------------
Config.dispatch = {
    enabled = false,
    system = 'default', -- Setting for the dispatch system to use ('default' for the built-in system or 'cd-dispatch', 'core-dispatch-old', 'core-dispatch-new' or 'ps-dispatch' for external systems)
    eventName = 'Cartel Robbed',
    blip = {
        sprite = 788,     -- Sprite for the blip
        color = 75,       -- Color for the blip
        scale = 1.0,      -- Scale for the blip
        alpha = 1.0,
        timeout = 60,     -- Time in seconds for the blip to disappear
        showRadar = true, -- Setting to show the radar blip on the radar
    },
}
Config                          =   {}                                                      
Config.debug                    =   false

-- Whether NPCs shoot at players.
Config.npcShoot                 =   true

-- Let players loot if only all items can be carried. (Except bags)
Config.canPlayerCarryAll        =   false

-- Render distance for the island.
Config.renderDistance           =   500.0

-- Model for boats.
Config.boatModel                =   'dinghy2'

-- Model for helicopter.
Config.helicopterModel          =   'buzzard'

-- Whether to output island reset logs to the server console.
Config.getConsoleOutput         =   false

-- Time interval for island reset in milliseconds.
Config.islandResetTime          =   3600000

-- Time interval for items reset in milliseconds.
Config.itemsResetTime           =   900000

-- Delay time for island reset if someone is on the island or in an interior in milliseconds.
Config.resetTimeDelay           =   60000

-- Cooldown time for interacting with interior enter/exit in milliseconds.
Config.interiorCooldown         =   2000



Config.target = {
    enabled = true,
    system = 'ox_target'    -- 'qtarget' or 'qb-target'  (Other systems might work as well)
}

--- SETTINGS FOR ESX
Config.esxSettings = {
    enabled = true,    
    useNewESXExport = true,
    account = 'money',
    oldEsx = false,
}

--- SETTINGS FOR QBCORE
Config.qbSettings = {
    enabled = false,
    UseNewQBExport = true,  -- Make sure to uncomment the old export inside fxmanifest.lua if you're still using it
    account = 'cash',
}

Config.alternativeIdentifier = {
    enabled = true,
    identifier = "discord"  -- OPTIONS: license, xbl, live, discord, fivem, license2
}

Config.sqlDriver = "mysql"

Config.interiorExitCoords = { x = -213.86, y = 6291.14, z = -39.16}


---------------------------------------------------
---                 Buyer options               
---------------------------------------------------

-- Define properties for the blip representing the buyer.
Config.buyer = {
    blip = {
        enabled = true,     -- Whether the blip is enabled or not.
        sprite  = 207,      -- Sprite ID for the blip on the map.
        color   = 81,       -- Color of the blip.
        alpha   = 255,      -- Transparency level of the blip.
        scale   = 1.0       -- Scale of the blip.
    },
    
    ped         = true,    -- Whether the ped is enabled or not.
    
    marker      = false,   -- Whether the marker is enabled or not.
    
    -- Define the location of the buyer.
    location = {
        x = 2525.48,        -- X-coordinate of the buyer's location.
        y = 4980.82,        -- Y-coordinate of the buyer's location.
        z = 44.85,          -- Z-coordinate of the buyer's location.
        heading = 57.77     -- Heading direction of the buyer.
    },
    
    -- Define color properties for the marker.
    ['MarkerColor'] = {
        r = 0,              -- Red component of the marker color.
        g = 100,            -- Green component of the marker color.
        b = 0,              -- Blue component of the marker color.
        a = 100             -- Alpha/transparency level of the marker color.
    }  
}

-- Configuration settings for drawing 3D text.

Config.Draw3dTextOptions = {
    fontId = 4,     -- ID of the font used for the 3D text.
    scaleX = 0.1,   -- Scale of the text on the X-axis.
    scaleY = 0.1    -- Scale of the text on the Y-axis.
}

-- Configuration settings for item prices.

-- The item prices are randomly generated within specified ranges using math.random.

Config.itemPrice = {
    ['ls_weed_block']   = math.random(250, 500),    -- Price range for weed blocks.
    ['ls_weed_bag']     = math.random(100, 250),    -- Price range for weed bags.
    ['ls_coke_block']   = math.random(1000, 2500),  -- Price range for cocaine blocks.
    ['ls_coke_powder']  = math.random(250, 500),    -- Price range for cocaine powder.
    ['ls_jewellery']    = math.random(1000, 1500)   -- Price range for jewellery.
}

-- Note: Instead of random prices, fixed constant prices could also be used.
-- For example:
-- Config.itemPrice = {
--     ['ls_weed_block']   = 350,    -- Fixed price for weed blocks.
--     ['ls_weed_bag']     = 150,    -- Fixed price for weed bags.
--     ['ls_coke_block']   = 2000,   -- Fixed price for cocaine blocks.
--     ['ls_coke_powder']  = 300,    -- Fixed price for cocaine powder.
--     ['ls_jewellery']    = 1200    -- Fixed price for jewellery.
-- }



-- Configuration settings for island coordinates.

Config.islandCoords = {
    hint = {
        enabled = true,     -- Whether the hint is enabled or not.
        color = 1,          -- Color of the hint.
        alpha = 128         -- Transparency level of the hint.
    },
    coords = {
        x = -1215.98,       -- X-coordinate of the island.
        y = 7100.97,        -- Y-coordinate of the island.
        z = -6.0,           -- Z-coordinate of the island.
        heading = 0.0       -- Heading direction of the island.
    }    
}

-- Configuration settings for entrance coordinates.

Config.entranceCoords = {
    coords = {
        x = 65.64,          -- X-coordinate of the entrance. (Offset from the island)
        y = 73.56,          -- Y-coordinate of the entrance. (Offset from the island)   
        z = 5.98            -- Z-coordinate of the entrance. (Offset from the island)
    }    
}

-- Configuration settings for keys.

-- Model for keys.
Config.key = {
    model                 =   'bkr_prop_jailer_keys_01a',
    blip = {
        enabled = true,     -- Whether the blip is enabled or not.
        sprite  = 71,       -- Sprite ID for the blip on the map.
        color   = 30,       -- Color of the blip.
        alpha   = 255,      -- Transparency level of the blip.
        scale   = 1.0,      -- Scale of the blip.
        time    = 60000,       -- Time in milliseconds (ms) after which the blip appears after the key spawns.
    }
}

-- Configuration settings for wire cutters.

Config.wireCutters = {    
    blip = {
        enabled = true,     -- Whether the blip is enabled or not.
        sprite  = 71,       -- Sprite ID for the blip on the map.
        color   = 30,       -- Color of the blip.
        alpha   = 255,      -- Transparency level of the blip.
        scale   = 1.0       -- Scale of the blip.
    },
    locations = {
        {
            coords = {
                x = -533.08,    -- X-coordinate of the wire cutter location.
                y = 5292.81,    -- Y-coordinate of the wire cutter location.
                z = 74.23,      -- Z-coordinate of the wire cutter location.
                xRot = 0.0,     -- X-rotation of the wire cutter.
                yRot = 0.0,     -- Y-rotation of the wire cutter.
                zRot = 180.0    -- Z-rotation of the wire cutter.
            }
        },
        -- Additional locations can be added here.
    }
}

-- Configuration settings for allowed melee weapons to open crates (to open crates faster).

Config.meleeWeapon = {
    allowed = {
        'weapon_hatchet',       
        'weapon_battleaxe',     
        'weapon_crowbar'        
    }
}


Config.cartelNPCModels = {
    'A_M_M_EastSA_01',
    'CSB_Ramp_mex',
    'IG_Hao',
    'IG_Hao_02',
    'IG_Ortega',
    'S_M_Y_Robber_01',
}


Config.thermite = {
    blip = {
        enabled = true,             -- Whether the blip is enabled or not.
        sprite  = 486,              -- Sprite ID for the blip on the map.
        color   = 30,               -- Color of the blip.
        alpha   = 255,              -- Transparency level of the blip.
        scale   = 1.0               -- Scale of the blip.
    },
    model = 'hei_prop_heist_thermite',    -- Model of the thermite item.
    thermite = {
        offset = {
            x = 0.0,                 
            y = -0.075,              
            z = 0.0,                 
            h = 0.0,                 
        },
        rotation = {
            x = 90.0,                
            y = 90.0,                
            z = 0.0,                 
        },
    },
    locations = {
        {
            coords = {
                x = 2352.90,         
                y = 3137.67,         
                z = 48.52,           
                xRot = -0.00,        
                yRot = 0.00,         
                zRot = 180.00        
            }
        },
        {
            coords = {
                x = 2356.49,         
                y = 3136.78,         
                z = 47.24,           
                xRot = 0.00,         
                yRot = 0.00,         
                zRot = -8.00         
            }
        }
    }
}


-- Configuration settings for cartel island NPCs (on-foot).

-- Warning: Coordinates supposed to be declared with offset from the island (by using command /getcoords)

Config.cartelIslandNPC = {
    coords = {
        {
            x = 0.96, y = 7.28, z = 6.12, heading = 250.65
        },
        {
            x = -83.44, y = -79.04, z = 7.13, heading = 147.53
        },
        {
            x = -84.18, y = -47.73, z = 6.65, heading = 61.15
        },
        {
            x = -81.57, y = -32.25, z = 6.95, heading = 265.19
        },
        {
            x = -64.10, y = -23.39, z = 6.64, heading = 253.83
        },
        {
            x = -51.83, y = -21.32, z = 5.87, heading = 132.69
        },
        {
            x = -20.58, y = -4.31, z = 5.86, heading = 344.85
        },
        {
            x = -22.46, y = 17.31, z = 5.88, heading = 218.78
        },
        {
            x = -53.27, y = -74.15, z = 6.83, heading = 163.31
        },
        {
            x = -63.61, y = -41.77, z = 5.86, heading = 125.37
        },
        {
            x = -30.07, y = -38.64, z = 5.86, heading = 271.91
        },
        {
            x = -33.67, y = -21.63, z = 5.86, heading = 23.95
        },
        {
            x = -23.32, y = -19.03, z = 5.86, heading = 165.53
        },
        {
            x = -45.64, y = 9.20, z = 5.65, heading = 274.37
        },
        {
            x = -43.89, y = 14.46, z = 5.63, heading = 237.23
        },
        
    }
}

-- Configuration settings for cartel island backup NPCs (on-foot).
-- Warning: Coordinates supposed to be declared with offset from the island (by using command /getcoords)

Config.cartelBackupNPC = {
    coords = {
        {
            x = -60.26, y = -55.05, z = 5.86, heading = 315.49
        },
        {
            x = -39.21, y = -55.20, z = 6.21, heading = 299.09
        },
        {
            x = -29.70, y = -26.33, z = 5.86, heading = 309.45
        },
        {
            x = -80.05, y = 24.85, z = 4.44, heading = 61.54 
        },
        {
            x = -70.12, y = 25.07, z = 3.84, heading = 51.23
        },
        {
            x = -41.70, y = 14.39, z = 5.77, heading = 358.75
        },
        {
            x = -53.68, y = 0.30, z = 3.59, heading = 25.49
        },
        {
            x = -51.83, y = -21.32, z = 5.87, heading = 132.69
        },
           
        
    }
}


-- Configuration settings for EMP blocker.

-- The "goTo" variables x and y define the specific side of the item where the player will approach to pick it up.

Config.empBlocker = {
    blip = {
        enabled = true,             -- Whether the blip is enabled or not.
        sprite  = 544,              -- Sprite ID for the blip on the map.
        color   = 30,               -- Color of the blip.
        alpha   = 255,              -- Transparency level of the blip.
        scale   = 1.0               -- Scale of the blip.
    },
    amountToSpawn = 4,              -- Amount of EMP blockers to spawn.
    locations = {                   -- Locations where EMP blockers spawn (not commented as per request).
        {
            coords = {
                x = 2393.36, 
                y = 3065.14, 
                z = 51.09, 
                xRot = 3.24, 
                yRot = -15.03, 
                zRot = 180.0
            },
            goTo = {
                x = 0.6,
                y = 0.6
            }
        },
        {   
            coords = {
                x = 2381.17,
                y = 3095.90, 
                z = 47.19,
                xRot = -0.00, 
                yRot = 0.00, 
                zRot = -0.00
            },
            goTo = {
                x = 0.0,
                y = 0.6
            }
        },
        {
            coords = {
                x = 2348.15,
                y = 3140.30, 
                z = 48.53,
                xRot = -0.00, 
                yRot = 0.00, 
                zRot = -0.00
            },
            goTo = {
                x = 0.0,
                y = -0.6
            }
        },
        {
            coords = {
                x = 2142.93,
                y = 2905.00, 
                z = 49.81,
                xRot = -0.00, 
                yRot = 0.00, 
                zRot = 120.00
            },
            goTo = {
                x = -0.0,
                y = -0.6
            }
        },
        {
            coords = {
                x = 2075.39,
                y = 2950.92, 
                z = 46.34,
                xRot = 0.00, 
                yRot = 0.00, 
                zRot = -48.00
            },
            goTo = {
                x = 0.0,
                y = -0.6
            }
        },
        {
            coords = {
                x = 2050.73,
                y = 2946.82, 
                z = 56.57,
                xRot = -0.00, 
                yRot = -0.00, 
                zRot = -112.00
            },
            goTo = {
                x = 0.0,
                y = -0.6
            }
        },
    }
}








--  .d8888b.   .d88888b.  888b    888 88888888888        d8888 8888888 888b    888 8888888888 8888888b.   .d8888b.  
-- d88P  Y88b d88P" "Y88b 8888b   888     888           d88888   888   8888b   888 888        888   Y88b d88P  Y88b 
-- 888    888 888     888 88888b  888     888          d88P888   888   88888b  888 888        888    888 Y88b.      
-- 888        888     888 888Y88b 888     888         d88P 888   888   888Y88b 888 8888888    888   d88P  "Y888b.   
-- 888        888     888 888 Y88b888     888        d88P  888   888   888 Y88b888 888        8888888P"      "Y88b. 
-- 888    888 888     888 888  Y88888     888       d88P   888   888   888  Y88888 888        888 T88b         "888 
-- Y88b  d88P Y88b. .d88P 888   Y8888     888      d8888888888   888   888   Y8888 888        888  T88b  Y88b  d88P 
--  "Y8888P"   "Y88888P"  888    Y888     888     d88P     888 8888888 888    Y888 8888888888 888   T88b  "Y8888P"  
                                                                                                              
                                                                                                                 

Config.spots = {
    {
        pos = {             
            x = -1250.93,
            y = 7086.32,
            z = 7.15,
            h = 87.5,
        },
        container = 'small',
    },
    {
        pos = {
            x = -1192.64 ,
            y = 7154.152 ,
            z = 6.06,
            h = 75.48,
        },
        container = 'small',
    },   
    {   
        pos = {
            x = -217.16,
            y = 6271.42,
            z = -39.05,
            h = 216.10,
        },
        container = 'small',
    },   
}

Config.containers = {
    ['small'] = {
        main = {
            model = 'prop_container_04mb',
            offset = {
                x = 0.0,
                y = 0.0,
                z = -1.0,
                h = 270.0,
            },
        },
        lock = {
            model = 'hei_prop_container_lock',
            offset = {
                x = 0.0,
                y = -3.45,
                z = 1.25,
                h = 0.0,
            },
            rotation = {
                x = 0.0,
                y = 0.0,
                z = 0.0,
            },
        },
        doorLeft = {
            model = 'prop_container_door_mb_l',
            offset = {
                x = -1.295,
                y = -3.4,
                z = 1.4,
            },
            rotation = {
                x = 0.0,
                y = 0.0,
                z = 0.0,
            },
        },
        doorRight = {
            model = 'prop_container_door_mb_r',
            offset = {
                x = 1.295,
                y = -3.4,
                z = 1.4,
            },
            rotation = {
                x = 0.0,
                y = 0.0,
                z = 0.0,
            },
        },
        doorRearLeft = {
            model = 'prop_container_door_mb_l',
            offset = {
                x = 1.295,
                y = 3.4,
                z = 1.4,
            },
            rotation = {
                x = 0.0,
                y = 0.0,
                z = 180.0,
            },
        },
        doorRearRight = {
            model = 'prop_container_door_mb_r',
            offset = {
                x = -1.295,
                y = 3.4,
                z = 1.4,
            },
            rotation = {
                x = 0.0,
                y = 0.0,
                z = 180.0,
            },
        },
    }
}








--  .d8888b.  8888888b.         d8888 88888888888 8888888888  .d8888b.  
-- d88P  Y88b 888   Y88b       d88888     888     888        d88P  Y88b 
-- 888    888 888    888      d88P888     888     888        Y88b.      
-- 888        888   d88P     d88P 888     888     8888888     "Y888b.   
-- 888        8888888P"     d88P  888     888     888            "Y88b. 
-- 888    888 888 T88b     d88P   888     888     888              "888 
-- Y88b  d88P 888  T88b   d8888888888     888     888        Y88b  d88P 
--  "Y8888P"  888   T88b d88P     888     888     8888888888  "Y8888P"  


-- Configuration settings for crate spawn spots.

Config.cratesSpots = {
    {
        pos = {
            x = -223.50,
            y =  6269.71,
            z = -39.00,
            h =  1.09,
        },
        crate = 'single',
    },
    {
        pos = {
            x = -229.59,
            y =  6279.60,
            z = -39.0,
            h =  272.4,
        },
        crate = 'single',
    },
    {
        pos = {
            x = -215.58,
            y =  6277.99,
            z = -39.0,
            h =  80.4,
        },
        crate = 'single',
    }
}

Config.crates = {
    ['single'] = {
        main = {
            model = 'prop_ld_crate_01',
            offset = {
                x =  0.0,
                y =  0.0,
                z = -1.0,
                h =  270.0,
            },
        },
        top = {
            model = 'prop_ld_crate_lid_01',
            offset = {
                x = 0.0,
                y = 0.0,
                z = 0.56,
            },
            rotation = {
                x = 0.0,
                y = 0.0,
                z = 0.0,
            },
        }
    }
}


-- Configuration settings for different types of crates and their properties.

Config.crateTypes = {
    { 
        type = 'weed',      -- Type of the crate.
        props = {
            'weed_block1',  -- List of props associated with the weed crate type.
            'weed_block2',
            'weed_bag1',
            'weed_bag2',
            'weed_bag3',
            'weed_bag4',
            'weed_bag5',
            'weed_bag6',
        }
    },
    { 
        type = 'coke',      -- Type of the crate.
        props = {
            'coke_block1',  -- List of props associated with the coke crate type.
            'coke_block2',
            'coke_block3',
            'coke_block4',
            'coke_block5',
            'coke_block6',
            'coke_block7',
            'coke_block8', 
        }   
    },
    { 
        type = 'money',     -- Type of the crate.
        props = {
            'money_block1', -- List of props associated with the money crate type.
            'money_block2',
            'money_block3',
            'money_block4',
            'money_block5',
            'money_block6',
        }
    }
}



-- Configuration settings for crate opening animations and tools.

Config.crateOpening = {
    tool = {
        time = 1500,                                        -- Minimal value: 1500 milliseconds.
        dict = 'melee@large_wpn@streamed_core',             -- Animation dictionary for the tool.
        anim = 'plyr_front_takedown_bat_headhit'            -- Animation name for the tool.
    },
    unarmed = {
        time = 30000,                                       -- Time duration for opening without tools.
        dict = 'anim@amb@clubhouse@tutorial@bkr_tut_ig3@',  -- Animation dictionary for unarmed opening.
        anim = 'machinic_loop_mechandplayer'                -- Animation name for unarmed opening.
    }
}




-- 8888888b.  8888888b.   .d88888b.  8888888b.   .d8888b.  
-- 888  "Y88b 888   Y88b d88P" "Y88b 888   Y88b d88P  Y88b 
-- 888    888 888    888 888     888 888    888 Y88b.      
-- 888    888 888   d88P 888     888 888   d88P  "Y888b.   
-- 888    888 8888888P"  888     888 8888888P"      "Y88b. 
-- 888    888 888 T88b   888     888 888              "888 
-- 888  .d88P 888  T88b  Y88b. .d88P 888        Y88b  d88P 
-- 8888888P"  888   T88b  "Y88888P"  888         "Y8888P"  



Config.inside = {}
Config.inside.bigDrop = {
    'money_crate1',
    'money_crate2',
    'weed_pallete1',
    'weed_pallete2',
    'coke_stack2'
}

Config.inside.drop = {
    'weed_block1',
    'weed_block2',
    'weed_bag1',
    'weed_bag2',
    'weed_bag3',
    'weed_bag4',
    'weed_bag5',
    'weed_bag6',
    'coke_block1',
    'coke_block2',
    'coke_block3',
    'coke_block4',
    'coke_block5',
    'coke_block6',
    'coke_block7',
    'coke_block8',    
    'money_one1',
    'money_block1',
    'money_block2',
    'money_block3',
    'money_block4',
    'money_block5',
    'money_block6',
}



Config.inside.items = {
    ['weed_pallete1'] = {
        model = 'hei_prop_heist_weed_pallet',        
        reward = 'ls_weed_block',
        amount =  1
    },
    ['weed_pallete2'] = {
        model = 'hei_prop_heist_weed_pallet_02',
        reward = 'ls_weed_block',
        amount = 1
    },
    ['weed_block1'] = {
        model = 'prop_weed_block_01',
        reward = 'ls_weed_block',
        amount = 1
    },
    ['weed_block2'] = {
        model = 'hei_prop_heist_weed_block_01b',
        reward = 'ls_weed_block',
        amount = 1
    },
    ['weed_bag1'] = {
        model = 'bkr_prop_weed_smallbag_01a',
        reward = 'ls_weed_bag',
        amount = 1
    },
    ['weed_bag2'] = {
        model = 'bkr_prop_weed_bigbag_open_01a',
        reward = 'ls_weed_bag',
        amount = 1
    },
    ['weed_bag3'] = {
        model = 'bkr_prop_weed_bigbag_01a',
        reward = 'ls_weed_bag',
        amount = 1
    },
    ['weed_bag4'] = {
        model = 'bkr_prop_weed_bigbag_02a',
        reward = 'ls_weed_bag',
        amount = 1
    },
    ['weed_bag5'] = {
        model = 'bkr_prop_weed_bigbag_03a',
        reward = 'ls_weed_bag',
        amount = 1
    },
    ['weed_bag6'] = {
        model = 'ba_prop_battle_weed_bigbag_01a',
        reward = 'ls_weed_bag',
        amount = 1
    },
    ['money_one1'] = {
        model = 'bkr_prop_scrunched_moneypage',
        reward = 'ls_money_one',
        amount = 1
    },
    ['money_block1'] = {
        model = 'ba_prop_battle_moneypack_02a',
        reward = 'ls_money_medium',
        amount = math.random(500,2500)
    },
    ['money_block2'] = {
        model = 'bkr_prop_money_sorted_01',
        reward = 'ls_money_medium',
        amount = math.random(500,2500)
    },
    ['money_block3'] = {
        model = 'bkr_prop_money_unsorted_01',
        reward = 'ls_money_medium',
        amount = math.random(500,2500)
    },
    ['money_block4'] = {
        model = 'bkr_prop_money_wrapped_01',
        reward = 'ls_money_medium',
        amount = math.random(500,2500)
    },
    ['money_block5'] = {
        model = 'bkr_prop_moneypack_03a',
        reward = 'ls_money_medium',
        amount = math.random(500,2500)
    },
    ['money_block6'] = {
        model = 'h4_prop_h4_cash_bag_01a',
        reward = 'ls_money_medium',
        amount = math.random(500,2500)
    },
    ['money_crate1'] = {
        model = 'ex_prop_crate_money_bc',
        reward = 'ls_money_big',
        amount = math.random(2500, 7500)
    },
    ['money_crate2'] = {
        model = 'ex_prop_crate_money_sc',
        reward = 'ls_money_big',
        amount = math.random(2500, 7500)
    },
    ['coke_block1'] = {
        model = 'prop_coke_block_half_a',
        reward = 'ls_coke_block',
        amount = 1
    },
    ['coke_block2'] = {
        model = 'prop_coke_block_half_b',
        reward = 'ls_coke_block',
        amount = 1
    },
    ['coke_block3'] = {
        model = 'prop_coke_block_01',
        reward = 'ls_coke_block',
        amount = 1
    },
    ['coke_block4'] = {
        model = 'bkr_prop_coke_block_01a',
        reward = 'ls_coke_block',
        amount = 1
    },
    ['coke_block5'] = {
        model = 'bkr_prop_coke_cut_01',
        reward = 'ls_coke_block',
        amount = 1
    },
    ['coke_block6'] = {
        model = 'bkr_prop_coke_cut_02',
        reward = 'ls_coke_block',
        amount = 1
    },
    ['coke_block7'] = {
        model = 'ba_prop_battle_coke_block_01a',
        reward = 'ls_coke_block',
        amount = 1
    },    
    ['coke_block8'] = {
        model = 'bkr_prop_coke_cutblock_01',
        reward = 'ls_coke_block',
        amount = 1
    },
    ['coke_stack2'] = {
        model = 'h4_prop_h4_coke_stack_01a',
        reward = 'ls_coke_powder',
        amount = 1
    }
}



-- 8888888 888b    888 88888888888 8888888888 8888888b.  8888888  .d88888b.  8888888b.  
--   888   8888b   888     888     888        888   Y88b   888   d88P" "Y88b 888   Y88b 
--   888   88888b  888     888     888        888    888   888   888     888 888    888 
--   888   888Y88b 888     888     8888888    888   d88P   888   888     888 888   d88P 
--   888   888 Y88b888     888     888        8888888P"    888   888     888 8888888P"  
--   888   888  Y88888     888     888        888 T88b     888   888     888 888 T88b   
--   888   888   Y8888     888     888        888  T88b    888   Y88b. .d88P 888  T88b  
-- 8888888 888    Y888     888     8888888888 888   T88b 8888888  "Y88888P"  888   T88b 
                                                                                     
Config.doorOpeningSpeed =  0.2   -- Adjust door opening speed [0.1 - 1.0]  0.1 - slow ; 1.0 - fast

Config.cardCoords = {
    x = -219.956116, 
    y = 6292.504883, 
    z = -38.935513
}

-- Configuration settings for interior NPC positions within the cartel area.

-- NOTE: These coordinates are not offset of the interior/island, plain coordinates. 
-- You can get your current coordinates by using command /getc

Config.cartelInteriorNPC = {
    coords = {
        {
            x = -225.52, y = 6286.673, z = -39.16, heading = 250.60   -- Position and heading for NPC.
        },
        {
            x = -229.25, y = 6281.79, z = -39.04, heading = 267.01     -- Position and heading for NPC.
        },
        {
            x = -218.10, y = 6268.12, z = -39.12, heading = 39.79      -- Position and heading for NPC.
        },
        {
            x = -232.94, y = 6272.31, z = -38.69, heading = 266.92     -- Position and heading for NPC.
        },
        {
            x = -215.31, y = 6273.74, z = -39.17, heading = 31.06      -- Position and heading for NPC.
        },
    }
}


Config.tableItems = {
    ['single_ring1'] = {
        model = 'prop_jewel_03a',        
        reward = 'ls_jewellery',
        amount =  1
    },
    ['single_ring2'] = {
        model = 'prop_jewel_03b',        
        reward = 'ls_jewellery',
        amount =  1
    },
    ['multiple_rings'] = {
        model = 'prop_jewel_pickup_new_01',
        reward = 'ls_jewellery',
        amount = 1
    },
    ['single_watch1'] = {
        model = 'prop_jewel_02c',
        reward = 'ls_jewellery',
        amount = 1
    },
    ['single_watch2'] = {
        model = 'prop_jewel_02b',
        reward = 'ls_jewellery',
        amount = 1
    },
    ['single_watch3'] = {
        model = 'prop_jewel_02a',
        reward = 'ls_jewellery',
        amount = 1
    },
    ['multiple_watches'] = {
        model = 'ex_office_swag_jewelwatch',
        reward = 'ls_jewellery',
        amount = 1
    },
    ['single_skull'] = {
        model = 'p_jewel_pickup33_s',
        reward = 'ls_jewellery',
        amount = 1
    },
    ['single_necklace1'] = {
        model = 'p_jewel_necklace01_s',
        reward = 'ls_jewellery',
        amount = 1
    },
    ['single_necklace2'] = {
        model = 'p_jewel_necklace_02',
        reward = 'ls_jewellery',
        amount = 1
    },
    ['single_necklace3'] = {
        model = 'p_jewel_necklace02_s',
        reward = 'ls_jewellery',
        amount = 1
    },
    ['single_sapphire'] = {
        model = 'sf_prop_sf_jewel_01a',
        reward = 'ls_jewellery',
        amount = 1
    },
    ['multiple_bracelets1'] = {
        model = 'prop_jewel_04a',
        reward = 'ls_jewellery',
        amount = 1
    },
    ['multiple_bracelets2'] = {
        model = 'prop_jewel_04b',
        reward = 'ls_jewellery',
        amount = 1
    },
    ['multiple_bracelets3'] = {
        model = 'ex_office_swag_jewelwatch2',
        reward = 'ls_jewellery',
        amount = 1
    },
}

Config.tables = {
    coords = {
        {x = -245.8, y = 6268.65, z = -38.29, heading = 90.0},
        {x = -245.79, y = 6272.02, z = -38.29, heading = 0.0},
        {x = -243.28, y = 6272.01, z = -38.29, heading = 0.0},        
        {x = -241.07, y = 6268.88, z = -38.29, heading = 90.0}
    }
}

Config.tableDrop = {
    {
        props = {
            ['single_ring1'] = {
                x = 0.3,
                y = -0.4,
                z = 0.05,
                heading = 0.0
            },
            ['single_watch1'] = {
                x = 0.3,
                y = -0.6,
                z = 0.05,
                heading = 0.0
            },
            ['single_skull'] = {
                x = 0.2,
                y = 0.525,
                z = 0.07,
                heading = 0.0
            },
            ['single_necklace3'] = {
                x = 0.15,
                y = 0.6,
                z = 0.02,
                heading = 0.0
            },
            ['single_necklace2'] = {
                x = 0.15,
                y = 0.8,
                z = 0.02,
                heading = 0.0
            },
            ['multiple_bracelets1'] = {
                x = -0.15,
                y = -0.5,
                z = 0.05,
                heading = 0.0
            },
            ['multiple_rings'] = {
                x = -0.1,
                y = -0.2,
                z = 0.02,
                heading = 0.0
            },
            ['multiple_watches'] = {
                x = -0.3,
                y = 0.0,
                z = 0.00,
                heading = 0.0
            },
            ['single_ring2'] = {
                x = 0.3,
                y = 0.5,
                z = 0.00,
                heading = 0.0
            },            
        }
    },
    {
        props = {
            ['single_ring1'] = {
                x = -0.4,
                y = 0.0,
                z = 0.05,
                heading = 0.0
            },
            ['single_watch1'] = {
                x = -0.3,
                y = 0.0,
                z = 0.05,
                heading = 0.0
            },
            ['single_skull'] = {
                x = 0.525,
                y = -0.5,
                z = 0.07,
                heading = 0.0
            },
            ['single_necklace3'] = {
                x = 0.3,
                y = 0.05,
                z = 0.02,
                heading = 0.0
            },
            ['single_necklace2'] = {
                x = 0.5,
                y = 0.05,
                z = 0.02,
                heading = 0.0
            },
            ['multiple_bracelets1'] = {
                x = -0.5,
                y = -0.15,
                z = 0.05,
                heading = 0.0
            },
            ['multiple_rings'] = {
                x = -0.2,
                y = -0.1,
                z = 0.02,
                heading = 0.0
            },
            ['multiple_watches'] = {
                x = 0.0,
                y = -0.3,
                z = 0.00,
                heading = 0.0
            },
            ['single_ring2'] = {
                x = 0.5,
                y = 0.0,
                z = 0.00,
                heading = 0.0
            },            
        }
    },
    {
        props = {
            ['single_ring1'] = {
                x = -0.4,
                y = 0.0,
                z = 0.05,
                heading = 0.0
            },
            ['single_watch1'] = {
                x = -0.3,
                y = 0.0,
                z = 0.05,
                heading = 0.0
            },
            ['single_skull'] = {
                x = 0.525,
                y = -0.5,
                z = 0.07,
                heading = 0.0
            },
            ['single_necklace3'] = {
                x = 0.3,
                y = 0.05,
                z = 0.02,
                heading = 0.0
            },
            ['single_necklace2'] = {
                x = 0.5,
                y = 0.05,
                z = 0.02,
                heading = 0.0
            },
            ['multiple_bracelets1'] = {
                x = -0.5,
                y = -0.15,
                z = 0.05,
                heading = 0.0
            },
            ['multiple_rings'] = {
                x = -0.2,
                y = -0.1,
                z = 0.02,
                heading = 0.0
            },
            ['multiple_watches'] = {
                x = 0.0,
                y = -0.3,
                z = 0.00,
                heading = 0.0
            },
            ['single_ring2'] = {
                x = 0.5,
                y = 0.0,
                z = 0.00,
                heading = 0.0
            },            
        }
    },
    {
        props = {
            ['single_ring1'] = {
                x = 0.3,
                y = -0.4,
                z = 0.05,
                heading = 0.0
            },
            ['single_watch1'] = {
                x = 0.3,
                y = -0.6,
                z = 0.05,
                heading = 0.0
            },
            ['single_skull'] = {
                x = 0.2,
                y = 0.525,
                z = 0.07,
                heading = 0.0
            },
            ['single_necklace3'] = {
                x = 0.15,
                y = 0.6,
                z = 0.02,
                heading = 0.0
            },
            ['single_necklace2'] = {
                x = 0.15,
                y = 0.8,
                z = 0.02,
                heading = 0.0
            },
            ['multiple_bracelets1'] = {
                x = -0.15,
                y = -0.5,
                z = 0.05,
                heading = 0.0
            },
            ['multiple_rings'] = {
                x = -0.1,
                y = -0.2,
                z = 0.02,
                heading = 0.0
            },
            ['multiple_watches'] = {
                x = -0.3,
                y = 0.0,
                z = 0.00,
                heading = 0.0
            },
            ['single_ring2'] = {
                x = 0.3,
                y = 0.5,
                z = 0.00,
                heading = 0.0
            },            
        }
    }
    
}

Config.palletesBags = {
    prop = 'h4_prop_h4_big_bag_01a',


    coords = {
        {
            x = 0.5, 
            y = 0.00, 
            z = 0.425, 
            heading = 15.0
        },
        {
            x = -0.5, 
            y = 0.25, 
            z = 0.425, 
            heading = 30.0
        },
        {
            x = 0.0, 
            y = 0.00, 
            z = 0.425, 
            heading = -30.0
        }
    },
    drop = {
        'weed_block',
        'weed_bag',
        'coke_block', 
        'money',
    } 
}


Config.palleteItems = {
    ['weed_block'] = {
        reward = 'ls_weed_block',
        amount = 1
    },
    ['weed_bag'] = {
        reward = 'ls_weed_bag',
        amount = 1
    },
    ['money'] = {
        reward = 'ls_money_medium',
        amount = math.random(500,2500)
    },
    ['coke_block'] = {
        reward = 'ls_coke_block',
        amount = 1
    },
}


Config.policeJobNames = {
    'police'
}
------------------------------------------
--- DISPATCH
------------------------------------------
Config.dispatch = {
    enabled = false,
    system = 'default', -- Setting for the dispatch system to use ('default' for the built-in system or 'cd-dispatch', 'core-dispatch-old', 'core-dispatch-new' or 'ps-dispatch' for external systems)
    eventName = 'Cartel Robbed',
    blip = {
        sprite = 788,     -- Sprite for the blip
        color = 75,       -- Color for the blip
        scale = 1.0,      -- Scale for the blip
        alpha = 1.0,
        timeout = 60,     -- Time in seconds for the blip to disappear
        showRadar = true, -- Setting to show the radar blip on the radar
    },

```
