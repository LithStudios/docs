# Config

Complete configuration reference for LS Smell.

## Framework Selection

```lua
Config.inventory = 'ox'
```

Options: `'ox'`, `'esx'`, `'qb'`, `'origen'`, `'ps'`, `'ak47'`

Sets which inventory framework to integrate with. You must also implement the framework-specific item detection in `client/item_detector.lua`.

## Global Settings

```lua
Config.global = {
    viewDistance = 5.0,
    trailUpdateInterval = 2000,
    syncInterval = 2000,
    decayCheckInterval = 5000,
    motionThreshold = 0.5,
    nighttimeAlphaIncrease = 0.2
}
```

### viewDistance

* Type: `number`
* Default: `5.0`
* Description: Maximum distance (in units) that particles are visible. Only particles within this distance from the player will be rendered.

### trailUpdateInterval

* Type: `number` (milliseconds)
* Default: `2000`
* Description: How often new trail points are created while moving. Lower values create more frequent trails but increase resource usage.

### syncInterval

* Type: `number` (milliseconds)
* Default: `2000`
* Description: How often trails are synchronized to the server for multiplayer visibility. Lower values provide smoother trails for other players but increase network traffic.

### decayCheckInterval

* Type: `number` (milliseconds)
* Default: `5000`
* Description: How often the system checks for expired trails to clean up. Higher values improve performance but may keep expired particles longer.

### motionThreshold

* Type: `number` (m/s)
* Default: `0.5`
* Description: Speed threshold for props to be considered "moving". Props above this speed will emit trails if `emitWhenMoving` is enabled.

### nighttimeAlphaIncrease

* Type: `number` (0.0 - 1.0)
* Default: `0.2`
* Description: Alpha value boost during nighttime hours (8pm-6am). Set to `0.2` for 20% increase in visibility at night.

## Particle Presets

Define reusable particle configurations:

```lua
Config.presets = {
    weed = {
        color = rgb(10, 220, 10),
        dict = 'core',
        particle = 'veh_respray_smoke',
        scale = 0.5,
        ttl = 60000
    },
    blood = {
        color = rgb(139, 0, 0),
        dict = 'core',
        particle = 'veh_respray_smoke',
        scale = 0.3,
        ttl = 120000
    }
}
```

### Preset Properties

#### color

* Type: `table` (RGB)
* Description: Particle color using `rgb(r, g, b)` helper function. Values range from 0-255.

#### dict

* Type: `string`
* Description: Particle dictionary asset name. Must be a valid FiveM particle asset.
* Common dicts: `'core'`, `'scr_rcbarry2'`, `'scr_trevor1'`

#### particle

* Type: `string`
* Description: Particle effect name within the dictionary.
* Common particles: `'veh_respray_smoke'`, `'exp_air_molotov'`

#### scale

* Type: `number`
* Default: `1.0`
* Description: Size multiplier for the particle effect.

#### ttl

* Type: `number` (milliseconds)
* Description: Time to live - how long the particle remains before expiring.

## Smelly Items

Configure items that emit trails when carried by players:

```lua
Config.smelly_items = {
    weed = {
        trailing_smell = {
            enable = true,
            distance = 1.0
        },
        preset = 'weed',
        ttl = 60000,
        offset = vector3(0, 0, -1.0)
    }
}
```

### Item Properties

#### trailing\_smell.enable

* Type: `boolean`
* Description: Whether this item should emit trails when carried.

#### trailing\_smell.distance

* Type: `number`
* Description: Minimum distance player must move before creating a new trail point. Prevents trail spam.

#### preset

* Type: `string`
* Description: Which preset from `Config.presets` to use for this item's particles.

#### ttl

* Type: `number` (milliseconds)
* Default: Uses preset TTL if not specified
* Description: Override the preset's TTL for this specific item.

#### offset

* Type: `vector3` (optional)
* Description: World-space offset for particle spawn position relative to player.

## Smelly Props

Configure objects/props that emit smell in the world:

```lua
Config.smelly_props = {
    prop_weed_01 = {
        emitWhenStationary = true,
        emitWhenMoving = true,
        preset = 'weed',
        ttl = 60000,
        viewDistance = 10.0
    }
}
```

### Prop Properties

#### emitWhenStationary

* Type: `boolean`
* Description: Whether to emit trails when the prop is not moving. Creates a trail every 5 seconds when stationary.

#### emitWhenMoving

* Type: `boolean`
* Description: Whether to emit trails when the prop is moving (speed above `motionThreshold`).

#### preset

* Type: `string`
* Description: Which preset from `Config.presets` to use for this prop's particles.

#### ttl

* Type: `number` (milliseconds)
* Default: Uses preset TTL if not specified
* Description: Override the preset's TTL for this specific prop.

#### viewDistance

* Type: `number` (optional)
* Default: Uses global viewDistance if not specified
* Description: Override the global viewDistance for this specific prop.

## Events

Configure events that trigger smell trails:

```lua
Config.events = {
    shooting = {
        enable = true,
        preset = 'gunpowder',
        ttl = 30000,
        attachToPlayer = true
    },
    CEventNetworkEntityDamage = {
        enable = true,
        preset = 'blood',
        ttl = 120000,
        attachToPlayer = true
    }
}
```

### Event Properties

#### enable

* Type: `boolean`
* Description: Whether this event should trigger smell trails.

#### preset

* Type: `string`
* Description: Which preset from `Config.presets` to use for this event's particles.

#### ttl

* Type: `number` (milliseconds)
* Default: Uses preset TTL if not specified
* Description: Override the preset's TTL for this specific event.

#### attachToPlayer

* Type: `boolean`
* Description: If `true`, the trail follows the player's position. If `false`, trail is created at the event location and stays there.

## Smell Mode

Configure the `/smellmode` command feature:

```lua
Config.smellMode = {
    enable = true,
    duration = 30000,
    cooldown = 60000,
    alphaMultiplier = 1.5,
    label = {
        enable = true,
        text = "~g~Smelly~s~",
        distance = 10.0
    }
}
```

### Smell Mode Properties

#### enable

* Type: `boolean`
* Default: `true`
* Description: Enable or disable the `/smellmode` command.

#### duration

* Type: `number` (milliseconds)
* Default: `30000`
* Description: How long the enhanced smell mode remains active.

#### cooldown

* Type: `number` (milliseconds)
* Default: `60000`
* Description: Cooldown period between smell mode activations.

#### alphaMultiplier

* Type: `number`
* Default: `1.5`
* Description: Multiplier for particle alpha during smell mode (1.5 = 50% brighter).

#### label.enable

* Type: `boolean`
* Default: `true`
* Description: Show 3D text labels above smelly props during smell mode.

#### label.text

* Type: `string`
* Default: `"~g~Smelly~s~"`
* Description: Label text shown above smelly props. Supports GTA text formatting codes.

#### label.distance

* Type: `number`
* Default: `10.0`
* Description: Maximum distance to show labels above smelly props.

## Helper Functions

The config includes helper functions for easier configuration:

### rgb(r, g, b)

Converts RGB values (0-255) to the format expected by particle functions.

```lua
color = rgb(255, 0, 0)
```

## Example Configurations

{% tabs %}
{% tab title="High Performance" %}
```lua
Config.global = {
    viewDistance = 3.0,
    trailUpdateInterval = 3000,
    syncInterval = 3000,
    decayCheckInterval = 10000,
    motionThreshold = 1.0,
    nighttimeAlphaIncrease = 0.15
}
```

Use this to reduce resource usage and network traffic at the cost of visual fidelity.
{% endtab %}

{% tab title="High Quality" %}
```lua
Config.global = {
    viewDistance = 10.0,
    trailUpdateInterval = 1000,
    syncInterval = 1500,
    decayCheckInterval = 3000,
    motionThreshold = 0.3,
    nighttimeAlphaIncrease = 0.25
}
```

Use this for more detailed and responsive trails with increased resource usage.
{% endtab %}

{% tab title="Roleplay-Focused" %}
```lua
Config.presets = {
    blood = {
        ttl = 300000
    }
}

Config.smellMode = {
    duration = 60000,
    alphaMultiplier = 2.0
}
```

Long-lasting trails suitable for detective/investigation gameplay.
{% endtab %}
{% endtabs %}
