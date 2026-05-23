---
description: Configuration file for pickpocketing
---

# Config

```lua
Config = {}

--Wheter to timeout player from pickpocketing npcs
Config.timeout = {
    enabled = true,
    max_attempts = 3, -- 
    duration = 120 -- seconds
}

--How much time player has to pickpocket
Config.time_to_pickpocket = {
    min = 20,   -- in seconds
    max = 30    -- in seconds
}

--Can only loot peds that are not walking
Config.still_peds_only = false

Config.bystanders = {
    --Wheter bystanders can call police on the player
    enabled = true,
    -- chance to call police per bystander
    chance = 100, -- in %
    time_to_report = 5, -- in seconds
    -- Whether to show blips on peds that are alerting police
    show_blips = true,
    -- Blip settings for reporting peds
    blip = {
        sprite = 280, -- Blip icon/sprite (280 = phone icon)
        color = 1, -- Blip color (1 = red)
        scale = 0.8 -- Blip scale
    }
}

-- % of the max element width
Config.safe_zone_width = {
    Easy = 50,    -- %
    Medium = 35,  -- %
    Hard = 25,    -- %
    Expert = 10   -- %
}

-- Whether exiting early from the minigame (ESC or close button) results in success or failure
Config.early_exit_success = true -- true = success, false = failure

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
        text = "Pickpocketing",
        flash = true
    }
}

Config.items = {
    {
        name = "ls_phone",
        label = 'Phone',
        image = '/images/phone.webp',
        amount = math.random(1, 2),
        difficulty = 'Expert'
    },
    {
        name = "ls_weed",
        label = 'Weed',
        image = '/images/weed.webp',
        amount = math.random(1, 2),
        difficulty = 'Easy'
    },
    {
        name = "ls_ash",
        label = 'Cash',
        image = '/images/cash.webp',
        amount = math.random(100, 1000),
        difficulty = 'Medium'
    },
    {
        name = "ls_lighter",
        label = 'Lighter',
        image = '/images/lighter.webp',
        amount = math.random(1, 2),
        difficulty = 'Easy'
    },
    {
        name = "ls_gummies",
        label = 'Gummies',
        image = '/images/gummies.webp',
        amount = math.random(1, 2),
        difficulty = 'Easy'
    },
    {
        name = "ls_receipt",
        label = 'Receipt',
        image = '/images/receipt.webp',
        amount = math.random(1, 2),
        difficulty = 'Medium'
    },
    {
        name = "ls_meth",
        label = 'Meth',
        image = '/images/meth.webp',
        amount = math.random(1, 2),
        difficulty = 'Hard'
    }
}
```
