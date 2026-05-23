---
description: A FiveM resource that visualizes smells through particle effects in-game.
---

# Smell visualization

Create immersive environmental effects with visible particle trails that decay over time, featuring multiplayer synchronization and framework integration.

## Features

* **Visual Particle Trails** - Creates visible particle effects that follow players and objects
* **Three Smell Sources** - Items being carried, props/objects in motion, and events (shooting, damage)
* **Time-Based Decay** - Trails automatically expire based on configurable TTL values
* **Multiplayer Sync** - State bag synchronization shows other players' smell trails
* **Distance-Based Culling** - Optimized performance with viewDistance-based rendering
* **Nighttime Enhancement** - Automatic alpha boost during night hours (8pm-6am)
* **Smell Mode Command** - `/smellmode` command for temporary enhanced visibility with 3D labels
* **Framework Compatible** - Supports ox, esx, qb, origen, ps, ak47 inventory frameworks
* **Preset System** - Reusable particle definitions for consistent effects
* **Custom Events** - Extensible event system for gamemode-specific smell triggers

## Framework Compatibility

* ox\_inventory
* ESX
* QBCore
* Origen
* Project Sloth
* AK47 Inventory
* Missing your framework? Reach out to us on our [discord](https://discord.gg/CMXznkWYxa)

## Installation

{% stepper %}
{% step %}
### Download & Install

Download the resource and extract to your `resources` folder.
{% endstep %}

{% step %}
### Enable Resource

Add the following to your `server.cfg`:

```
ensure ls_smell
```
{% endstep %}

{% step %}
### Configure Inventory Framework

Open `config.lua` and set your inventory framework.
{% endstep %}

{% step %}
### Integrate Item Detection

Edit `Config.inventory` to match your server's framework.
{% endstep %}

{% step %}
### Restart Server

Restart your server to load the resource.
{% endstep %}
{% endstepper %}

## Quick Start

{% stepper %}
{% step %}
### Basic Configuration

Set your inventory framework in `config.lua`:

{% code title="config.lua" %}
```lua
Config.inventory = 'ox'
```
{% endcode %}
{% endstep %}

{% step %}
### Adding Smelly Items

Configure items that emit trails when carried:

{% code title="config.lua (smelly items)" %}
```lua
Config.smelly_items = {
    weed = {
        trailing_smell = {
            enable = true,
            distance = 1.0
        },
        preset = 'weed',
        ttl = 60000
    }
}
```
{% endcode %}
{% endstep %}

{% step %}
### Adding Smelly Props

Configure objects/props that emit smell:

{% code title="config.lua (smelly props)" %}
```lua
Config.smelly_props = {
    prop_weed_01 = {
        emitWhenStationary = true,
        emitWhenMoving = true,
        preset = 'weed',
        ttl = 60000
    }
}
```
{% endcode %}
{% endstep %}

{% step %}
### Framework Integration Example

Edit `client/item_detector.lua` and implement the `IsPlayerCarryingItem()` function for your framework:

{% code title="client/item_detector.lua" %}
```lua
function IsPlayerCarryingItem(player, itemName)
    -- Example for ox_inventory
    local count = exports.ox_inventory:Search('count', itemName)
    return count > 0
end
```
{% endcode %}

See the `client/editables/` folder for framework-specific examples.
{% endstep %}
{% endstepper %}

## In-Game Commands

* `/smellmode` - Activates enhanced smell visibility mode with 3D labels above smelly props

## Performance

* Distance-based particle rendering (only within viewDistance)
* Automatic trail expiration based on TTL
* Props checked only within 50 units of player
* State bags only updated when player has active trails
* Optimized distance calculations using squared distance

## Support

{% hint style="info" %}
For support and updates, visit [Lith Studios Discord](https://discord.gg/lithstudios)
{% endhint %}

