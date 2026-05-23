---
description: >-
  A dynamic robbery script that allows players to snatch items from NPCs and
  targeted locations with an interactive minigame system and risk-reward
  mechanics.
---

# Snatch & grab

## Overview

**Version:** 1.0.11\
**Author:** Lith Studios | Swizz\
**Type:** Crime Script\
**Framework:** Standalone (inventory integration recommended)

## Features

* Interactive snatch minigame with directional controls
* Multiple target types (NPCs, shops, street vendors)
* Risk-based difficulty scaling
* Police dispatch integration with wanted levels
* Dynamic NPC reaction system
* Item randomization with value tiers
* Cooldown management for repeated attempts
* Blip tracking for wanted NPCs
* Configurable target locations
* Multi-language locale support
* Debug mode for development

## Installation

1. Place `ls_snatch` in your resources folder
2. Configure the script (see Configuration section)
3. Add to server.cfg:

```cfg
ensure ls_snatch
```

4. Restart your server

## Dependencies

* Required:
  * None (standalone)
* Recommended:
  * Framework (ESX/QBCore) for inventory integration
  * Dispatch system for police alerts
  * Wanted level system

## Configuration

Located in `server/editables/editables.lua` and `client/editables/editables.lua`

### Main Configuration

#### Target Types

```lua
Config.target_types = {
    npc = {
        enabled = true,
        min_distance = 1.0,
        interact_distance = 2.5,
    },
    shop = {
        enabled = true,
        min_distance = 5.0,
        interact_distance = 3.0,
    },
    street_vendor = {
        enabled = true,
        min_distance = 2.0,
        interact_distance = 2.0,
    },
}
```

#### Minigame Settings

```lua
Config.minigame = {
    time_to_snatch = {
        min = 15,
        max = 25,
    },
    difficulty_scaling = true,
    early_exit_allowed = true,
}
```

#### Difficulty Configuration

```lua
Config.difficulty = {
    Easy = {
        safe_zone = 45,
        witness_chance = 30,
        police_response = 'Low',
    },
    Medium = {
        safe_zone = 35,
        witness_chance = 60,
        police_response = 'Medium',
    },
    Hard = {
        safe_zone = 20,
        witness_chance = 90,
        police_response = 'High',
    },
}
```

#### NPC Reaction System

```lua
Config.npc_reactions = {
    enabled = true,
    pursuit_enabled = true,
    chase_distance = 100,
    give_up_distance = 150,
    call_police_chance = 75,
}
```

#### Police System

```lua
Config.police = {
    enabled = true,
    dispatch_system = 'cd_dispatch',
    wanted_level = {
        1 = 1,  -- Easy snatch = 1 star
        2 = 2,  -- Medium snatch = 2 stars
        3 = 3,  -- Hard snatch = 3 stars
    },
    response_time = 10,
}
```

#### Cooldown System

```lua
Config.cooldown = {
    enabled = true,
    duration = 300,  -- 5 minutes per target
    location_based = true,
}
```

### Loot Configuration

Configure snatchable items:

```lua
Config.items = {
    {
        name = 'cash_small',
        label = 'Small Cash',
        amount = {min = 50, max = 150},
        difficulty = 'Easy',
        weight = 10,
    },
    {
        name = 'cash_large',
        label = 'Large Cash',
        amount = {min = 200, max = 500},
        difficulty = 'Medium',
        weight = 25,
    },
    {
        name = 'gold_chain',
        label = 'Gold Chain',
        amount = {min = 1, max = 2},
        difficulty = 'Hard',
        weight = 5,
    },
    {
        name = 'jewelry_bag',
        label = 'Jewelry Bag',
        amount = {min = 1, max = 1},
        difficulty = 'Hard',
        weight = 15,
    },
}
```

### Target Locations

```lua
Config.target_locations = {
    {
        name = 'Downtown Vendor 1',
        coords = vector3(200.5, -900.2, 24.1),
        type = 'street_vendor',
        difficulty = 'Easy',
    },
    {
        name = 'Clothing Store',
        coords = vector3(415.2, -982.1, 29.4),
        type = 'shop',
        difficulty = 'Medium',
    },
    {
        name = 'Jewelry District',
        coords = vector3(100.5, 50.3, 71.7),
        type = 'shop',
        difficulty = 'Hard',
    },
}
```

## How It Works

### Player Experience

{% stepper %}
{% step %}
### Target Selection

* Identify snatchable target (NPC or location)
* Target marked with blip (if configured)
{% endstep %}

{% step %}
### Initiation

* Approach target within interaction range
* Press interaction key to start
{% endstep %}

{% step %}
### Minigame

* Directional control system appears
* Player must follow on-screen prompts
* Time limit: 15-25 seconds (random)
* Can exit early (configurable)
{% endstep %}

{% step %}
### Outcome

* Success: Items added to inventory
* Failure: Wanted level applied
* Consequences: Police dispatch, NPC pursuit
* Cooldown: Location locked for duration
{% endstep %}

{% step %}
### Escape

* Evade NPCs and police
* Hide or travel distance to evade
{% endstep %}
{% endstepper %}

### Risk-Reward System

* Easy targets: Low wanted level, common items
* Medium targets: Moderate wanted level, valuable items
* Hard targets: High wanted level, rare items

Higher difficulty = greater risk but better rewards

## Usage Examples

### Basic Snatch

{% stepper %}
{% step %}
Locate street vendor in downtown
{% endstep %}

{% step %}
Approach within interaction range
{% endstep %}

{% step %}
Press E to start snatch minigame
{% endstep %}

{% step %}
Complete directional prompts
{% endstep %}

{% step %}
Receive items on success
{% endstep %}

{% step %}
Escape area before police arrive
{% endstep %}
{% endstepper %}

### Shop Robbery

{% stepper %}
{% step %}
Target clothing or jewelry store
{% endstep %}

{% step %}
Initiate snatch at counter
{% endstep %}

{% step %}
Witness alert triggers
{% endstep %}

{% step %}
NPC pursues or calls police
{% endstep %}

{% step %}
Get wanted level based on difficulty
{% endstep %}

{% step %}
Hide for cooldown period
{% endstep %}
{% endstepper %}

### Evading Police

{% stepper %}
{% step %}
Escape pursuit after failed snatch
{% endstep %}

{% step %}
Leave wanted level area
{% endstep %}

{% step %}
Hide for 60 seconds
{% endstep %}

{% step %}
Wanted level decreases
{% endstep %}

{% step %}
Return to continue activities
{% endstep %}
{% endstepper %}

## Customization

### Adding Custom Targets

```lua
table.insert(Config.target_locations, {
    name = 'Market Stall',
    coords = vector3(x, y, z),
    type = 'street_vendor',
    difficulty = 'Easy',
})
```

### Adjusting Difficulty

Make easier:

```lua
Config.difficulty.Medium.safe_zone = 45
Config.minigame.time_to_snatch.max = 20
```

Make harder:

```lua
Config.difficulty.Easy.safe_zone = 25
Config.minigame.time_to_snatch.max = 30
```

### Disable Police Response

```lua
Config.police.enabled = false
```

### Modify Cooldown Duration

```lua
Config.cooldown.duration = 600  -- 10 minutes
```

### Enable NPC Pursuit

```lua
Config.npc_reactions.pursuit_enabled = true
Config.npc_reactions.chase_distance = 150
```

## Police Integration

### cd\_dispatch

```lua
Config.police.dispatch_system = 'cd_dispatch'
-- Automatically integrated with dispatch events
```

### Custom Integration

Modify event in `client/client.lua`:

```lua
-- Police alert event
TriggerServerEvent('dispatch:snatch_alert', coords, difficulty)
```

## Troubleshooting

<details>

<summary>Minigame Not Starting</summary>

* Verify target coordinates are correct
* Check interaction distance settings
* Ensure script is fully loaded
* Check console for Lua errors

</details>

<details>

<summary>Items Not Appearing</summary>

* Verify item names in loot table
* Check inventory integration
* Confirm weight limits not exceeded
* Enable debug mode

</details>

<details>

<summary>Police Not Responding</summary>

* Check dispatch system configuration
* Verify police job exists on server
* Confirm wanted level system active
* Review dispatch integration logs

</details>

<details>

<summary>NPC Not Pursuing</summary>

* Enable `Config.npc_reactions.pursuit_enabled`
* Verify chase distance settings
* Check NPC model availability
* Confirm reaction system enabled

</details>

## Debug Mode

Enable debug output:

```lua
-- In config:
Config.debug = true
```

Debug information includes:

* Target detection
* Minigame events
* Item spawning
* Police dispatch calls
* NPC reactions
* Cooldown tracking

## Performance

* Optimized target scanning - Only checks nearby locations
* Efficient minigame - Lightweight UI system
* Smart NPC pathfinding - Limited pursuit range
* Idle: 0.00ms
* Active: 0.02-0.03ms
* Minigame active: 0.05ms

## Locale Support

Customize text in `locale/en.lua`:

```lua
Locale = {
    ['snatch_start'] = 'Starting snatch minigame...',
    ['snatch_success'] = 'Snatch successful!',
    ['snatch_failed'] = 'Snatch failed!',
    ['police_alert'] = 'Police dispatched to your location!',
    ['cooldown_active'] = 'Too many recent thefts here!',
    ['npc_pursuing'] = 'The NPC is chasing you!',
    -- ... more strings
}
```

## API Reference

### Events

Client Events:

* `snatch:start` - Start snatch minigame
* `snatch:success` - Snatch completed successfully
* `snatch:failed` - Snatch attempt failed

Server Events:

* `snatch:reward` - Give player items
* `snatch:police_alert` - Dispatch police
* `snatch:npc_reaction` - NPC response

### Exports

Currently no exports. Future versions may include:

* `AddCustomTarget()` - Register custom snatch target
* `IsTargetOnCooldown()` - Check target cooldown status

## Support

For issues or questions:

* Enable debug mode first
* Check console for errors
* Review configuration
* Contact Lith Studios support

## Changelog

**v1.0.11** - Latest

* Improved NPC pathfinding
* Enhanced police integration
* Added difficulty scaling
* Fixed cooldown system

**v1.0.0** - Initial Release

* Basic snatch mechanics
* Minigame system
* Police integration
