---
description: Configuration file to viewable props
---

# Config

```lua
Config = {}

Config.debug = false

Config.framework = 'esx' -- esx or qbcore

Config.useNewESXExport = true

Config.useNewQBExport = true

Config.target = {
    enabled = true,
    system = 'ox_target' -- 'qtarget' or 'qb-target' or 'ox_target'  (Other systems might work as well)
}

-- Keybind for interacting with objects eg. "Press E to look at menu"
Config.keybind = 'E'

-- Default scenario that plays when looking at an image
Config.playerScenario = {
    enabled = true, -- Setting to enable the player scenario for the card
    scenario = 'WORLD_HUMAN_CLIPBOARD'  -- Player scenario for the card usage
}

-- If there are 2 identical props in a given radius it deletes one of them.
-- Recommend to enable this when you are trying to set the correct position of the prop
Config.deleteCloseProps = {
    enable = false,
    radius = 5.0
}

--- MAKE SURE TO DELETE/EDIT THE EXAMPLE PROPS PROVIDED BELOW
--- Arguments
-- name = name of the prop that will spawn
-- fileUrl = direct url to the image that will be visible
-- size = size of the image that will be shown in percentage (1 - 100)
-- OPTIONAL (add them inside the sub-table):
-- scenario = scenario that will override default scenario when player is looking at an image
-- jobs = table of jobs that will be able to access the image
-- targetDistance = distance from which player can interact with the object using targeting (Must be a float!)
-- spawn = false -- this will prevent the prop from spawning
Config.objects = {
    {
        name = 'prop_sign_interstate_03',
        label = 'staff_1_dead',
        size = 90,
        targetDistance = 3.0,
        scenario = 'WORLD_HUMAN_TOURIST_MAP',
        targetIcon = "fa-solid fa-user",
        targetLabel = 'Podívat se na obrázek',
        customText = 'Podívat se na obrázek',
        spawn = true,
        fileUrl = "https://cdn-blog.novoresume.com/articles/cv-examples/Professional-CV-Template.png",
        coords = {
            x = -254.1,
            y = -983.1,
            z = 31.1,
            h = 225.8538
        }
    },
}

--- LOCALE
-- To translate the messages edit the message on the right side! Not the message between the square brackets
Locale = {
    ['~r~You can not view this'] = '~r~You can not view this',
}
```
