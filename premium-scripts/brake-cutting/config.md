---
description: Configuration file for brake cutting. Found in `ls_brake_cutting/config.lua`.
---

# Config

```lua
Config = {}

-- Type in 'esx' or 'qbcore' depending on your framework
-- Type in '' if you are using standalone version
Config.framework = 'esx'

Config.debug = true

Config.useNewESXExport = true

--Set useCommand to true if you are using standalone version of the script
Config.command = {
    useCommand = true,
    commandName = 'brakeCut'
}
--If vehicle's brakes can be disabled if someone is inside a vehicle
Config.canDisableIfVehicleOccupied = true

--If item should be one time use
Config.toolOneTimeUse = true

Config.brakeCutting = {
    -- how long the player has to search before cutting brakes (in ms)
    searchingTime = 5500,
    -- how many inputs player has to make before brakes get cut
    cuttingLength = 30,
    -- how long player has to wait before attempting to cut brakes again (in ms)
    cuttingMessedUpDuration = 5000,
    -- inputs player has to make to successfully cut the brakes
    cuttingKeybinds = {
        'A',
        'D',
    }
}
-- If player should be able to use handbrake when brakes fail
Config.disableHandbrake = true

--Item that is used to cut the brakes
Config.toolName = 'ls_wirecutters'

--These vehicles' brakes can not be cut
Config.blacklistedVehicles = {
    'police',
    'ambulance'
}

Config.particles = {
    --If particles should fly out of wheels when brakes fail
    particlesOn = true,
    --Particle scale
    scale = 1.0,
    --Particle dictionary
    dict = 'core',
    particle = 'veh_train_sparks'
}

-- How long player has to brake for the brakes to fail
Config.brakingTime = 500

--ilfk
```
