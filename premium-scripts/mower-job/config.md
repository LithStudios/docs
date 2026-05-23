---
description: Configuration file for mower job
---

# Config

```lua
Config = {}

Config.alternativeIdentifier = {
    enabled = true,
    identifier = "discord"  -- OPTIONS: license, xbl, live, discord, fivem, license2
}

Config.sqlDriver = "mysql"

--- SETTINGS FOR ESX
Config.esxSettings = {
    enabled = true,
    oldEsx = false,
    account = 'money',
}

--- SETTINGS FOR QBCORE
Config.qbSettings = {
    enabled = false,
    UseNewQBExport = false,  -- Make sure to uncomment the old export inside fxmanifest.lua if you're still using it
    account = 'cash',
}

--- SETTINGS FOR STANDALONE 
Config.standaloneSettings = {
    enabled = false,
    payment = false,
}


Config.target = {
    enabled = false,
    system = 'ox_target'    -- 'qtarget' or 'qb-target'  (Other systems might work as well)
}

Config.debugMode = {
    debug = false,
    debugLocationIndex = 1     -- when debugging choose first location index to check
}

Config.job = {
    enabled = false,
    jobName = 'mower',
}

Config.rocksAmount = {
    min = 5,                -- Minimal amount of rocks to spawn
    max = 19,               -- Maximal amount of rocks to spawn
    damagePerRock = 50.0,   -- Damage to mower per one rock
}

Config.grassAmount = {
    min = 10,               -- Minimal amount of grass to spawn
    max = 30,               -- Maximal amount of grass to spawn
}

Config.percentage = {
    enabled = false,        -- toggle turn on/off this feature
    minPercent = 0.15,      -- what percent of grass cut is acceptable to get payed 
}

Config.mowerMovingAnim = {
    duration = 2000
}

Config.mowerSpeed = { 
    default = 1.4,          -- starting mower speed 
    levelUp = 1.3           -- mower speed increases by given number with level up   
}                           -- NOTE: Units are in meters per second!

Config.grassModels = {
    'prop_veg_grass_01_a',
    'prop_grass_dry_02',
    'prop_veg_grass_01_c',
}

Config.rockModels = {
    'rock_4_cl_2_2',
}

Config.vehiclesModels = {
    truck = 'sadler',       
    trailer = 'trailersmall',
    mower = 'mower'
}

Config.qbInteract = {
    distance = 3.5, -- distance to interact with mower
}

Config.vehiclesSpawning = {
    vehiclesCount = 3,      -- how many vehicles you wish to use (2[truck + mower]) 3([truck+trailer+mower])

    truck = {
        x = -173.1445,      
        y = -51.271,        
        z = 53.492,         
        heading = 157.06    
    },
    trailer = {             -- if you're using 2 vehicles only, these coords won't change anything.
        x = -171.5,        
        y = -45.703,       
        z = 52.54393,      
        heading = 78.694    
    },    
    attachmentOffset = {
        x = 0.0,            -- change where on truck your mower is gonna attach (offset from the boot)
        y = -1.0,
        z = 0.5,
    },
    mowerOff = {            -- configure mower detach coords ( offset from mower )
        {
            x = -2.5,       -- left side
            y = 0.0,
            z = -1.0,
        },
        {
            x = 2.5,        -- right side
            y = 0.0,
            z = -1.0,
        },
        {
            x = 0.0,        -- rear
            y = -4.5,
            z = -1.0,
        },
    },    
}

Config.jobMarkersAndBlips = {
    ['distanceJobMarker'] = 20.0    -- Marker radius
    ,
    ['jobMarkerColor'] = {
        r = 0,      -- red
        g = 100,    -- green
        b = 0,      -- blue
        a = 100,    -- alpha/transparency
    },
    ['jobBlipSettings'] = {
        headquarters = {
            x = -153.903, 
            y = -41.235, 
            z = 54.326, 
            heading = 95.497
        },

        configure = {
            sprite = 71,
            color = 25,
            alpha = 255,
            scale = 1.0,
        }
    },
}



Config.mainJobPlace = {
    showJobPlaceBlip = true,    -- choose to show blip or not
    detectDistance = 30.0       -- distance to detect vehicles from (to return deposit for vehicles)
}

Config.levelTable = {
    [1] = 100,    -- Level 1 1-100       beginner
    [2] = 250,    -- Level 2 100-250     intermediate
    [3] = 750,    -- Level 3 250-750     advanced
    [4] = 1500,   -- Level 4 750-1500    master
    [5] = 2000,   -- Level 5 1500-2000   grass artist
}

Config.levelNames = {
    [1] = { name = "Beginner" },
    [2] = { name = "Intermediate" },
    [3] = { name = "Advanced" },
    [4] = { name = "Master" },
    [5] = { name = "Grass Artist" }
}

  
Config.experience = {
    perRock = 1,                -- Experience increasement for single rock picked up
    perGrass = 1,               -- Experience increasement for single grass cut
    extra = 10,                 -- Extra experiece player gets for fully cutting the grass.
}

Config.payments = {
    --reward = 5,  -- payment for one cut grass
    reward = math.random(15, 45), -- payment for job is from interval [15 to 45]
    bonus = 170,
    depositForVehicles = 100,
}


Config.locations = {
    --1
    {   
        coords = {
            x = -1315.29,
            y = 172.92,
            z = 58.02
        },
        pedCoords = {
            x = -1341.66,
            y = 161.57,
            z = 57.79,
            heading = 297.0
        },
        radius = {
            from = -10,
            to = 10,
        },
        blacklistedAreas = {            
        
        }
    },
        --2
    {
        coords = {
            x = -782.512,
            y = -940.36,
            z = 17.48
        },
        pedCoords = {
            x = -769.69,
            y = -932.81,
            z = 17.94,
            heading = 160.7
        },
        radius = {
            from = -10,
            to = 10,
        },
        blacklistedAreas = {
       
        }
    
    },
        --3
    {
        coords = {
            x = -1051.695,
            y = -683.10,
            z = 22.844
        },
        pedCoords = {
    
            x = -1054.36,
            y = -703.99,
            z = 20.94,
            heading = 287.54
        },
        radius = {
            from = -10,
            to = 10,
        },
        blacklistedAreas = {

        }
    
    
    },
    
    
    --4--
    {
        coords = {
            x = -1301.893,
            y = -1435.82,
            z = 4.21
        },
        pedCoords = {
            x = -1301.83,
            y = -1419.19,
            z = 4.54,
            heading = 352.6
        },
        radius = {
            from = -10,
            to = 10,
        },
        blacklistedAreas = {

        }
    },
    --5


    {
        coords = {
            x = -1329.69,
            y = -1360.884,
            z = 4.425
        },
        pedCoords = {
            x = -1324.43,
            y = -1356.55,
            z = 4.79,
            heading = 279.28
        },
        radius = {
            from = -10,
            to = 10,
        },
        blacklistedAreas = {

        }
    },
      --6
      {
        coords = {
            x = -810.15,
            y = 861.17,
            z = 202.59
        },
        pedCoords = {
            x = -799.35,
            y = 865.67,
            z = 203.16,
            heading = 132.41
        },
        radius = {
            from = -10,
            to = 10,
        },
        blacklistedAreas = {

        }
    },
    --7
    {
        coords = {
            x = 1010.668,
            y = 226.648,
            z = 82.904
        },
        pedCoords = {
            x = 1007.966, 
            y = 219.4, 
            z = 82.29, 
            heading = 239.159
        },
        radius = {
            from = -10,
            to = 10,
        },
        blacklistedAreas = {
            {
                x = 1002.91,
                y = 219.673, 
                z = 82.77,
                radius = 2.8
            },                  -- blacklisted areas are the areas where grass won't spawn with a given radius
            {
                x = 1014.977,
                y = 231.231,
                z = 82.986,
                radius = 4.0
            }
        }
    },
    
    --8
    {
        coords = {
            x = 915.355,
            y = 109.89,
            z = 79.02
        },
        pedCoords = {
            x = 915.355,
            y = 109.89,
            z = 79.02,
            heading = 155.35
        },
        radius = {
            from = -10,
            to = 10,
        },
        blacklistedAreas = {

        }
    },
    --9
    {        
        coords = {
            x = 1276.0,
            y = -643.50,
            z = 68.14,
        },
        pedCoords = {
            x = 1278.781,
            y = -651.6232,
            z = 67.72,
            heading = 338.68,
        },
        radius = {
            from = -7,
            to = 7,
        },
        blacklistedAreas = {

        }
    },
    --10
    {   
        coords = {
            x = -678.364,
            y = -1853.236,
            z = 29.523
        },
        pedCoords = {
            x = -689.702,
            y = -1843.449,
            z = 29.00031, 
            heading = 202.093
        },
        radius = {
            from = -7,
            to = 7
        },
        blacklistedAreas = {
 
        }
    },
    --11
    {   
        coords = {
            x = -699.614,
            y = -1655.592,
            z = 25.166
        },
        pedCoords = {
            x = -687.185,
            y = -1661.338,
            z = 24.897, 
            heading = 15.525
        },
        radius = {
            from = -7,
            to = 7
        },
        blacklistedAreas = {
  
        }
    },
    --12
    {
        coords = {
            x = -606.011, 
            y = -1312.524, 
            z = 11.864
        },
        pedCoords = {
            x = -609.720, 
            y = -1302.114, 
            z = 11.446, 
            heading = 159.302
        },
        radius = {
            from = -7,
            to = 7
        },
        blacklistedAreas = {

        }
    },
    --13
    {
        coords = {
            x = -793.808, 
            y = -25.058, 
            z = 38.910
        },
        pedCoords = {
            x = -790.582, 
            y = -36.146, 
            z = 37.987, 
            heading = 52.070
        },
        radius = {
            from = -7,
            to = 7
        },
        blacklistedAreas = {
   
        }
    },
    --14
    {
        coords = {
            x = -677.253, 
            y = -35.667, 
            z = 38.372
        },
        pedCoords = {
            x = -678.201, 
            y = -45.674, 
            z = 38.131, 
            heading = 105.680
        },
        radius = {
            from = -7,
            to = 7
        },
        blacklistedAreas = {
   
        }
    },
    
   
}

```
