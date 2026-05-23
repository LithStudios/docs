---
description: >-
  A FiveM resource for postal locker theft activities. Players can hack into
  postal locker units, break open individual cells, and loot items with various
  minigames and interactions.
---

# Features

## Features

* **Hacking Minigame**: Brute force attack minigame to unlock postal locker units
* **Cell Breaking**: Sequence minigame to break open individual locker cells
* **Loot System**: Randomized loot generation with different package sizes (small, medium, large)
* **Carry System**: Players can carry large loot items and loot them later
* **Dispatch Integration**: Automatic police dispatch alerts when hacking fails
* **Reset System**: Automatic cooldown and reset system for lockers
* **Multiple Models**: Support for PostOp and GoPostal locker models
* **Visual Effects**: Particle effects when breaking cells
* **State Synchronization**: Client-server state synchronization using GlobalState

***

## Installation

### Prerequisites

1. **kq\_link** - This script requires kq\_link to be installed and running
   * Download: https://github.com/Kuzkay/kq\_link
   * Make sure it's started before this resource

### Steps

1. Place the `ls_locker_theft` folder in your `resources/[lith]` directory
2. Ensure the resource name is exactly `ls_locker_theft` (the script checks for this)
3. Add to your `server.cfg`:

```cfg
ensure kq_link
ensure ls_locker_theft
```

4. Configure the script in `config.lua` (see Configuration section)
5. Restart your server or start the resource

***

## Configuration

### Basic Settings

```lua
Config.debug = false  -- Enable debug mode
```

### Locker Locations

Configure locker positions in `Config.lockers`:

```lua
Config.lockers = {
    {
        coords = vector3(47.676, 99.946, 77.903),
        rotation = vector3(0.3, -0.8, 68.9),
        size = 2,  -- 1 for small (15 cells), 2 for large (30 cells)
        model = 2  -- 1 for PostOp, 2 for GoPostal
    },
    -- Add more lockers...
}
```

Parameters:

* `coords`: World position of the locker
* `rotation`: Rotation vector for the locker
* `size`: `1` = small (15 cells), `2` = large (30 cells)
* `model`: `1` = PostOp model, `2` = GoPostal model

### Input Controls

Customize key bindings in `Config.inputs`:

```lua
Config.inputs = {
    drop = {
        key = 'X',
        control = '~INPUT_VEH_DUCK~'
    },
    loot = {
        key = 'E',
        control = '~INPUT_CONTEXT~'
    },
    hack = {
        key = 'F',
        control = '~INPUT_VEH_DUCK~'
    },
    pick_up = {
        key = 'E',
        control = '~INPUT_CONTEXT~'
    },
    break_in = {
        key = 'L',
        control = '~INPUT_CONTEXT~'
    }
}
```

### Loot Configuration

#### Loot Times

Time required to loot items based on size:

```lua
Config.loot_times = {
    small = 2,   -- seconds
    medium = 3, -- seconds
    large = 5   -- seconds
}
```

#### Loot Props

Define which props appear for each size category:

```lua
Config.props = {
    ['small'] = {
        'prop_drug_package_02',
        'm23_2_prop_m32_package_01a',
        -- Add more...
    },
    ['medium'] = {
        'v_ret_gc_ammo5',
        -- Add more...
    },
    ['large'] = {
        'v_res_filebox01',
        -- Add more...
    }
}
```

#### Prop Attachment

Configure how large props attach to players:

```lua
Config.prop_attach = {
    ['v_res_filebox01'] = {
        offset = vector3(0.08, 0.12, -0.27),
        rotation = vector3(166, 69, -257),
        ped_bone = 0xDEAD
    },
    -- Add more...
}
```

#### Loot Generation

```lua
Config.loot = {
    empty_cell_chance = 10,  -- % chance cell has no loot prop
    empty_loot_chance = 20,  -- % chance loot prop has no items

    amounts = {
        small = { min = 1, max = 2 },
        medium = { min = 2, max = 3 },
        large = { min = 4, max = 6 }
    },

    items = {
        small = {
            ['phone'] = { 1, 5 },      -- [min, max] amount
            ['money'] = { 1, 5 },
            ['mastercard'] = { 1, 5 },
            ['clothing'] = { 1, 5 },
        },
        -- Configure medium and large similarly...
    }
}
```

### Minigame Configuration

#### Hacking Minigame

```lua
Config.hack = {
    code_length = 4,    -- Length of code to guess
    max_attempts = 8,  -- Maximum attempts allowed
    timer_length = 90  -- Time limit in seconds
}
```

#### Sequence Minigame (Cell Breaking)

```lua
Config.sequence = {
    min = 1,  -- Minimum number of keys in sequence
    max = 6   -- Maximum number of keys in sequence
}
```

### Reset Cooldown

```lua
Config.locker_reset_cooldown = {
    value = 10,
    units = 'minutes'  -- 'minutes' or 'seconds'
}
```

### Visual Effects

```lua
Config.particles = {
    enable = true,
    particle_asset = 'core',
    particle_name = 'ent_anim_dusty_hands',
    particle_scale = 2.0,
    particle_play_length = 2000  -- milliseconds
}
```

### Dispatch System

```lua
Config.dispatch = {
    enabled = true,
    jobs = { 'police', 'bsco', 'lspd' },  -- Jobs that receive alerts
    blip = {
        sprite = 4,
        color = 1,
        scale = 1.5,
        text = L('dispatch_blip_message'),
        flash = false
    }
}
```

***

## Gameplay Mechanics

{% stepper %}
{% step %}
### Hacking the Locker Unit

* Approach a postal locker unit
* Press the hack key (default: `F`) when prompted
* A camera view focuses on the locker
* Complete the brute force hacking minigame:
  * Enter a 4-digit code
  * Receive feedback on each digit (correct position, wrong position, or not in code)
  * You have 8 attempts and 90 seconds
* If successful, all cells in the locker unlock
* If failed, a dispatch alert is sent (if enabled)
{% endstep %}

{% step %}
### Breaking Open Cells

* After hacking, approach any cell door
* Press the break-in key (default: `L`)
* Complete the sequence minigame (1-6 key presses)
* If successful, the cell door opens and reveals loot (if any)
* Particle effects play when the door breaks
{% endstep %}

{% step %}
### Looting Items — Small/Medium Items

* Approach the loot prop
* Press the loot key (default: `E`)
* Wait for the progress bar to complete
* Items are automatically added to inventory
{% endstep %}

{% step %}
### Looting Items — Large Items

* Approach the large loot prop
* Press the pick-up key (default: `E`)
* The prop attaches to your character
* Walk around carrying it
* Press loot key (default: `E`) to loot it, or drop key (default: `X`) to drop it
* When looting, a progress bar appears and items are added to inventory
{% endstep %}

{% step %}
### Reset System

* After a locker is hacked, it enters a cooldown period (default: 10 minutes)
* During cooldown, the locker cannot be hacked again
* After cooldown expires, the locker resets:
  * All cells close
  * New loot is generated
  * Hacking becomes available again
{% endstep %}
{% endstepper %}

***

## Customization

### Adding New Loot Items

1. Edit `Config.loot.items` in `config.lua`:

```lua
Config.loot.items = {
    small = {
        ['your_item'] = { 1, 5 },  -- [min, max]
        -- ...
    }
}
```

2. Ensure your item system supports `kq_link:AddPlayerItem` export

### Adding New Locker Locations

Add entries to `Config.lockers`:

```lua
{
    coords = vector3(x, y, z),
    rotation = vector3(rx, ry, rz),
    size = 1 or 2,
    model = 1 or 2
}
```

### Customizing Loot Props

1. Add prop models to `Config.props` under appropriate size category
2. If it's a large prop, add attachment configuration to `Config.prop_attach`

### Modifying Minigames

* **Hacking**: Edit `Config.hack` and modify `nui/index.html` for UI changes
* **Sequence**: Edit `Config.sequence` values

### Changing Rewards System

Modify `GiveReward()` function in `server/editables/loot.lua` to integrate with your item framework.

***

## Troubleshooting

<details>

<summary>Lockers Not Spawning</summary>

* Check that locker models are in your streaming files
* Verify coordinates are correct in `Config.lockers`
* Enable `Config.debug = true` to see error messages

</details>

<details>

<summary>Interactions Not Working</summary>

* Ensure `kq_link` is installed and running
* Check that the resource name is exactly `ls_locker_theft`
* Verify key bindings in `Config.inputs`

</details>

<details>

<summary>Loot Not Appearing</summary>

* Check `Config.loot` configuration
* Verify `empty_cell_chance` and `empty_loot_chance` aren't too high
* Ensure item names match your item system

</details>

<details>

<summary>Hacking Minigame Not Showing</summary>

* Check browser console for errors (F8 in-game)
* Verify NUI files are loading (`nui/index.html`)
* Ensure `SetNuiFocus` is working correctly

</details>

<details>

<summary>Dispatch Not Working</summary>

* Verify `kq_link` dispatch export is available
* Check `Config.dispatch.jobs` matches your job names
* Ensure dispatch is enabled: `Config.dispatch.enabled = true`

</details>

<details>

<summary>Performance Issues</summary>

* The script uses chunked entity checking for performance
* Large numbers of lockers may impact performance
* Consider reducing locker count or optimizing distance checks

</details>

***

## Notes

* The script uses GlobalState for client-server synchronization
* Locker units are only loaded when players are within 150 units
* Large loot items use networked entities for multiplayer sync
* The resource name must be exactly `ls_locker_theft` (checked on client start)
* Some files are marked as `escrow_ignore` for customization

***

## Support

For issues or questions, contact Lith Studios or check the original resource page.
