---
description: Configuration file for Real-time image placer.
---

# Config

```lua
Config = {}

Config.debug = false

Config.renderDistance = 300 -- Setting below 100 images will lose fade in/fade out effect

--Either DB or JSON
Config.dataType = 'DB'

Config.framework = 'esx' --type in esx, qbcore, qbox or standalone

Config.useNewESXExport = true

Config.offsetSliderAmount = 0.01 -- Adjusts by how many units you can adjust image's offset from the wall

Config.gif = {
    enable = true, -- Enable local gifs to be posted

    --- WARNING! Popular gif sites (GIPHY, TENOR, etc.) usually do not provide RAW gif links
    --- This means your gif's might end up looking like this: https://imgur.com/a/hKIKI24
    --- If you know a good website that provides RAW GIF links, let me know!
    enableLinks = true,
}

Config.images = {
    enableHiddenImages = true,
    enableJobOnlyImages = true
}

Config.devModePermissions = {
    --Members of these jobs will be able to access 'devmode' command
    jobs = {
        -- {
        --     name = 'police',
        --     minimumRank = 3, -- Minimum Rank Needed to access 'devmode',
        --     maxSizeX = 1.0, -- Maximum width allowed for images placed by this faction (Delete this for unlimited size)
        --     maxSizeY = 1.5, -- Maximum height allowed for images placed by this faction (Delete this for unlimited size)
        -- },
        -- {
        --     name = 'real_estate',
        --     minimumRank = 3
        -- }
    }
}

Config.sqlDriver = 'mysql'  -- mysql or oxmysql

-- Only used for discord webhooks (server/editable/server_config.lua)
-- If you do not understand - leave this as it is
Config.identifier = "license"-- OPTIONS: license, xbl, live, discord, fivem, license2

Config.commandNames = {
    devMode = 'devmode',
    deleteImage = 'deleteimage',
    disableImages = 'disableimages',

    -- By default admins bypass hidden images and job only images.
    -- Use this command to turn off/on access to these images (other admins are NOT impacted by this command!)
    disableAdminAccess = 'adminDisable'
}
--Keybind for selecting image points
Config.keybinds = {
    label = 'E',
    name = 'INPUT_PICKUP',
    input = "E",
}

--Maximum raycast distance
Config.raycastDistance = 30


```
