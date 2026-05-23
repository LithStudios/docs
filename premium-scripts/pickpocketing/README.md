---
description: >-
  A feature-rich pickpocketing script that allows players to steal items from
  NPCs using a difficulty-based minigame system.
---

# Pickpocketing

## Features

* Interactive pickpocketing minigame with moving safe zones
* Dynamic loot table with difficulty-based rewards
* Bystander witness system with police reporting
* Timeout/cooldown system to prevent spam
* Police dispatch integration
* Early exit option with configurable success/failure
* Blip system for reporting NPCs
* Multi-language locale support

## Installation

1. Place `ls_pickpocket` in your resources folder
2. Configure the script (see Configuration section)
3.  Add to server.cfg:

    ```cfg
    ensure ls_pickpocket
    ```
4. Restart your server

## Dependencies

* **Required:**
  * None (standalone)
* **Recommended:**
  * Framework (ESX/QBCore) for inventory integration
  * Dispatch system for police alerts

## Configuration

Located in `server/editables/editables.lua` and `client/editables/editables.lua`

### Main Configuration

#### Timeout System

```lua
Config.timeout = {
    enabled = true,           -- Enable cooldown system
    max_attempts = 3,         -- Maximum attempts before timeout
    duration = 120,           -- Timeout duration in seconds
}
```

#### Minigame Settings

```lua
Config.time_to_pickpocket = {
    min = 20,  -- Minimum game duration (seconds)
    max = 30,  -- Maximum game duration (seconds)
}

Config.early_exit_success = true  -- Exit early = automatic success
```

#### Difficulty Configuration

Safe zone width determines difficulty:

```lua
Config.safe_zone_width = {
    Easy = 50,     -- 50% safe zone
    Medium = 35,   -- 35% safe zone
    Hard = 25,     -- 25% safe zone
    Expert = 10,   -- 10% safe zone (very difficult)
}
```

#### Bystander System

```lua
Config.bystanders = {
    enabled = true,
    chance = 100,              -- Percentage chance of report (1-100)
    time_to_report = 5,        -- Seconds before calling police
    show_blips = true,         -- Show blip on reporting NPCs
    blip = {
        sprite = 161,
        color = 1,
        scale = 0.8,
    },
}
```

#### NPC Selection

```lua
Config.still_peds_only = false  -- Only allow pickpocketing stationary NPCs
```

### Loot Table Configuration

Configure items in the loot table:

```lua
Config.items = {
    {
        name = 'wallet',
        label = 'Wallet',
        image = 'wallet.png',
        amount = {min = 1, max = 1},
        difficulty = 'Easy',
    },
    {
        name = 'phone',
        label = 'Phone',
        image = 'phone.png',
        amount = {min = 1, max = 1},
        difficulty = 'Medium',
    },
    {
        name = 'jewelry',
        label = 'Jewelry',
        image = 'jewelry.png',
        amount = {min = 1, max = 3},
        difficulty = 'Hard',
    },
    {
        name = 'rolex',
        label = 'Rolex Watch',
        image = 'rolex.png',
        amount = {min = 1, max = 1},
        difficulty = 'Expert',
    },
}
```

### Police Dispatch

```lua
Config.dispatch = {
    enable = true,
    system = 'cd_dispatch',    -- 'cd_dispatch', 'ps-dispatch', etc.
    alertChance = 75,          -- Percentage chance of alert
    policeCode = '10-60',
    description = 'Pickpocketing in progress',
    blip = {
        sprite = 161,
        color = 1,
        scale = 1.0,
    },
    timeout = 60,              -- Blip duration (seconds)
}
```

## How It Works

### Player Experience

{% stepper %}
{% step %}
### Target NPC

* Player approaches an NPC
* Initiates pickpocket action
{% endstep %}

{% step %}
### Minigame

* Moving bar appears on screen
* Player must keep cursor in safe zone
* Duration: 20-30 seconds (random)
* Can exit early (configurable success/failure)
{% endstep %}

{% step %}
### Outcome

* **Success:** Receives random loot based on difficulty
* **Failure:** No items obtained
* **Witnesses:** Nearby NPCs may report to police
* **Cooldown:** Timeout applied if max attempts reached
{% endstep %}

{% step %}
### Police Response

* Dispatch alert sent (if configured)
* Police respond to location
* Blip shows on police map
{% endstep %}
{% endstepper %}

### Difficulty System

Item rewards are tied to difficulty levels:

* **Easy:** Common items (wallets, small cash)
* **Medium:** Moderate value items (phones, cards)
* **Hard:** Valuable items (jewelry, electronics)
* **Expert:** Rare/expensive items (luxury watches, diamonds)

Difficulty affects:

* Safe zone width in minigame
* Item rarity in loot pool
* Potential reward value

## Usage Examples

### Basic Pickpocketing

{% stepper %}
{% step %}
Approach any NPC on the street
{% endstep %}

{% step %}
Press interaction key
{% endstep %}

{% step %}
Complete the minigame
{% endstep %}

{% step %}
Receive items on success
{% endstep %}
{% endstepper %}

### Timeout System

After 3 failed attempts (default):

* Player is locked out for 120 seconds
* Timer displays remaining cooldown
* Can resume after timeout expires

### Witness Reporting

When witnesses are enabled:

* Nearby NPCs can report the crime
* 100% chance by default (configurable)
* 5-second delay before reporting
* Blip appears on reporting NPC
* Police dispatch triggered

## Customization

### Adding New Items

{% stepper %}
{% step %}
Open loot table configuration
{% endstep %}

{% step %}
Add new item entry:

```lua
{
    name = 'item_id',
    label = 'Display Name',
    image = 'item_image.png',
    amount = {min = 1, max = 5},
    difficulty = 'Medium',  -- Easy, Medium, Hard, Expert
}
```
{% endstep %}
{% endstepper %}

### Adjusting Difficulty

Make the minigame easier:

```lua
Config.safe_zone_width.Hard = 35  -- Increase safe zone
Config.time_to_pickpocket.min = 15  -- Reduce duration
```

Make it harder:

```lua
Config.safe_zone_width.Easy = 30  -- Reduce safe zone
Config.time_to_pickpocket.min = 25  -- Increase duration
```

### Disable Bystanders

```lua
Config.bystanders.enabled = false
```

### Modify Cooldown

```lua
Config.timeout = {
    enabled = true,
    max_attempts = 5,      -- More attempts
    duration = 60,         -- Shorter timeout
}
```

## Dispatch Integration

### cd\_dispatch

```lua
Config.dispatch.system = 'cd_dispatch'

-- Automatically integrated
```

### ps-dispatch

```lua
Config.dispatch.system = 'ps-dispatch'

-- Configure in dispatch resource
```

### Custom Dispatch

Modify event in `client/client.lua`:

```lua
-- Find dispatch trigger
TriggerServerEvent('your-dispatch:pickpocket', coords)
```

## Troubleshooting

<details>

<summary>Minigame Not Appearing</summary>

* Check browser console for errors (F8)
* Verify NUI resources are loading
* Ensure script is fully started

</details>

<details>

<summary>No Items Received</summary>

* Check loot table configuration
* Verify item names match inventory
* Enable debug mode to check item spawning

</details>

<details>

<summary>Bystanders Not Reporting</summary>

* Verify `Config.bystanders.enabled = true`
* Check police job configuration
* Ensure dispatch system is running

</details>

<details>

<summary>Timeout Not Working</summary>

* Verify `Config.timeout.enabled = true`
* Check console for errors
* Ensure max\_attempts is set correctly

</details>

## Debug Mode

Enable debug output:

```lua
-- In config:
Config.debug = true
```

Debug information includes:

* NPC detection
* Minigame events
* Item rewards
* Timeout tracking
* Bystander detection

## Performance

* **Optimized NPC detection** - Only checks nearby NPCs
* **Efficient minigame** - Lightweight UI
* **Smart witness system** - Limited radius checks
* **Idle:** 0.00ms
* **Active:** 0.01-0.02ms

## Locale Support

Customize text in `locale/en.lua` (or your language):

```lua
Locale = {
    ['pickpocket_start'] = 'Pickpocketing...',
    ['pickpocket_success'] = 'You successfully pickpocketed!',
    ['pickpocket_failed'] = 'Pickpocket attempt failed!',
    ['timeout_active'] = 'You must wait %s seconds',
    -- ... more strings
}
```

## API Reference

### Exports

Currently no exports. Future versions may include:

* `StartPickpocket(ped)` - Start pickpocket on specific ped
* `IsInTimeout(playerId)` - Check if player is in timeout

## Support

For issues or questions:

* Enable debug mode first
* Check console for errors
* Review configuration
* Contact Lith Studios support

## Changelog

**v1.0.0** - Initial Release

* Four difficulty levels
* Bystander witness system
* Timeout/cooldown system
* Police dispatch integration
* Multi-language support
