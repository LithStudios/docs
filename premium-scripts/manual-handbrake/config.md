---
description: Configurable file for manual handbrake.
---

# Config

```lua
Config = {}

Config.handbrake_alert = true

-- Full control list is available here: https://docs.fivem.net/docs/game-references/controls/
Config.handbrake_input = {
    enabled = true,
    --Handbrake can only be interacted with when vehicle's engine is off
    when_engine_off = false,
    control = 76,
    name = '~INPUT_VEH_HANDBRAKE~'
}

-- Roll speed multiplier
Config.roll_speed = 1.0

--The angle at which a vehicle will start to roll at
Config.angle_threshold = 5 -- percentage

--Define vehicle classes or specific models for vehicles which will not roll back on a hill
Config.automatic_handbrake_vehicles = {
    --List of all vehicle classes can be found here: https://wiki.rage.mp/wiki/Vehicle_Classes
    classes = {
       'Boats',
       'Sedans',
       'Super',
       'Bikes',
       'Cycles'
    },

    models = {
        'sultan',
        'ambulance'
    }
}
```
