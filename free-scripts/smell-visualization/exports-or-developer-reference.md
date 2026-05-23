# Exports | Developer reference

Available exports for custom integration and advanced usage of LS Smell.

## Client Exports

All exports are called from other resources using:

```lua
exports['ls_smell']:ExportName(params)
```

### AddItemTrail

Manually create an item trail at a specific location.

```lua
exports['ls_smell']:AddItemTrail(itemType, coords)
```

Parameters:

* `itemType` (string) - The item identifier matching a key in `Config.smelly_items`
* `coords` (vector3) - World coordinates where the trail should be created

Returns: `nil`

Example:

```lua
local playerCoords = GetEntityCoords(PlayerPedId())
exports['ls_smell']:AddItemTrail('weed', playerCoords)
```

Use Cases:

* Custom inventory drops
* Special event triggers
* Script-controlled smell emissions

***

### AddPropTrail

Manually create a prop trail for a specific entity.

```lua
exports['ls_smell_2']:AddPropTrail(propModel, entity, coords)
```

Parameters:

* `propModel` (string) - The prop model name matching a key in `Config.smelly_props`
* `entity` (number) - The entity handle of the prop
* `coords` (vector3) - World coordinates where the trail should be created

Returns: `nil`

Example:

```lua
local prop = GetClosestObjectOfType(coords, 2.0, GetHashKey('prop_weed_01'), false, false, false)
local propCoords = GetEntityCoords(prop)
exports['ls_smell_2']:AddPropTrail('prop_weed_01', prop, propCoords)
```

Use Cases:

* Custom prop spawning systems
* Dynamic object tracking
* Script-controlled prop smell emissions

***

## Custom Exports (No Config Required)

These exports allow you to create trails with custom particle settings without needing to define them in `config.lua`.

### AddCustomTrail

Create a trail at any coordinates with custom particle settings.

```lua
exports['ls_smell_2']:AddCustomTrail(coords, particleData, options)
```

Parameters:

* `coords` (vector3) - World coordinates where the trail should be created
* `particleData` (table) - Particle configuration with required keys:
  * `dict` (string) - Particle dictionary asset name
  * `particle` (string) - Particle effect name
  * `color` (table) - RGB color table: `{r = 0-255, g = 0-255, b = 0-255}`
  * `scale` (number, optional) - Size multiplier (default: 0.3)
  * `ttl` (number, optional) - Time to live in milliseconds (default: 5000)
  * `alpha` (number, optional) - Alpha transparency 0.0-1.0 (default: uses base alpha)
  * `offset` (vector3, optional) - World-space offset from coords
* `options` (table, optional) - Additional options:
  * `sourceId` (string, optional) - Custom source identifier (default: player server ID)
  * `itemType` (string, optional) - Custom item type identifier (default: auto-generated)
  * `checkDistance` (boolean, optional) - Whether to check distance before creating trail (default: true)

Returns: `boolean` - true if trail was created successfully

Example:

```lua
local success = exports['ls_smell_2']:AddCustomTrail(
    vector3(100.0, 200.0, 30.0),
    {
        dict = 'core',
        particle = 'veh_respray_smoke',
        color = {r = 255, g = 0, b = 0},
        scale = 0.5,
        ttl = 10000,
        alpha = 0.3,
        offset = vector3(0, 0, 0.5)
    },
    {
        itemType = 'my_custom_smell',
        checkDistance = true
    }
)
```

Use Cases:

* Custom gameplay mechanics without config modifications
* Dynamic trail generation from scripts
* Temporary smell effects for events
* Integration with third-party systems

***

### AddCustomPropTrail

Create a trail for any prop entity with custom particle settings.

```lua
exports['ls_smell_2']:AddCustomPropTrail(propEntity, particleData, options)
```

Parameters:

* `propEntity` (number) - The entity handle of the prop
* `particleData` (table) - Same as AddCustomTrail (dict, particle, color, scale, ttl, alpha, offset)
* `options` (table, optional) - Additional options:
  * `sourceId` (string, optional) - Custom source identifier (default: "prop\_{model}\_{entity}")
  * `itemType` (string, optional) - Custom item type identifier (default: auto-generated)
  * `checkDistance` (boolean, optional) - Whether to check distance before creating trail (default: true)
  * `motionThreshold` (number, optional) - Speed threshold for motion detection (default: from config)
  * `emitWhenMoving` (boolean, optional) - Emit when prop is moving (default: true)
  * `emitWhenStationary` (boolean, optional) - Emit when prop is stationary (default: true)

Returns: `boolean` - true if trail was created successfully

Example:

```lua
local prop = GetClosestObjectOfType(coords, 5.0, GetHashKey('prop_weed_01'), false, false, false)

local success = exports['ls_smell_2']:AddCustomPropTrail(
    prop,
    {
        dict = 'core',
        particle = 'veh_respray_smoke',
        color = {r = 0, g = 255, b = 0},
        scale = 0.3,
        ttl = 5000
    },
    {
        emitWhenStationary = true,
        emitWhenMoving = false,
        itemType = 'custom_prop_smell'
    }
)
```

Use Cases:

* Dynamic prop tracking without config
* Temporary smell effects on props
* Script-controlled prop smell emissions
* Custom prop spawning systems

***

### GetActiveParticleHandles

Returns all currently active particle handles in the system.

```lua
local handles = exports['ls_smell']:GetActiveParticleHandles()
```

Parameters: None

Returns: `table` - Map of particle handles with structure:

```lua
{
    ["sourceId_itemType_timestamp"] = {
        handle = number,
        coords = vector3,
        alpha = number,
        expiryTime = number
    }
}
```

Example:

```lua
local handles = exports['ls_smell']:GetActiveParticleHandles()
for id, data in pairs(handles) do
    print(string.format("Particle %s at %s with alpha %.2f", id, data.coords, data.alpha))
end
```

Use Cases:

* Custom visualization systems
* Debugging particle state
* Analytics/statistics tracking
* Integration with other detection systems

***

## Integration Examples

### Custom Drug Script Integration

```lua
function OnLootDrugs(drug_name)
    local player = PlayerPedId()
    local coords = GetEntityCoords(player)
    exports['ls_smell']:AddItemTrail(drug_name, coords)
end
```

### Smell Detection System

Create a system that detects nearby smells for gameplay mechanics:

```lua
function GetNearbySmells(coords, radius)
    local nearbySmells = {}
    local handles = exports['ls_smell']:GetActiveParticleHandles()

    for id, data in pairs(handles) do
        local distance = #(coords - data.coords)
        if distance <= radius then
            local itemType = id:match("_%d+_(%w+)_")
            table.insert(nearbySmells, {
                type = itemType,
                coords = data.coords,
                distance = distance,
                alpha = data.alpha
            })
        end
    end

    return nearbySmells
end

local playerCoords = GetEntityCoords(PlayerPedId())
local smells = GetNearbySmells(playerCoords, 5.0)

for _, smell in ipairs(smells) do
    print(string.format("Detected %s at distance %.2f", smell.type, smell.distance))
end
```
