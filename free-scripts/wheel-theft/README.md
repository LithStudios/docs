# Wheel theft

## Overview

`ls_wheel_theft` adds an interactive wheel‑theft mission to your FiveM server. Players can:

* Start a wheel theft mission at a configurable NPC.
* Receive a pickup truck (optional) and a random target vehicle at one of several locations.
* Jack up the target vehicle using a jack stand item or a command.
* Dismount and steal all four wheels via a bolt mini‑game.
* Load stolen wheels into the pickup truck.
* Deliver wheels to a seller NPC and get paid.
* Optionally trigger police dispatch / alerts when theft occurs.

Supports **ESX** and **QBCore** (toggleable), with job‑based permissions to raise/lower vehicles and to receive dispatch alerts.

Main files:

* `fxmanifest.lua` – resource manifest, script order.
* `config.lua` – all configurable options (framework, jobs, peds, payouts, locations, blips, locale, settings).
* `client/` – client logic (missions, UI, animations, props, jack stands, police alerts, truck spawn).
* `server/` – server logic (payouts, jack stand state, dispatch, framework integration).
* `_esx_setup/item.sql` – example ESX item definition for the jack stand.
* `_esx_setup/jack_stand.png` / `_qb_setup/jack_stand.png` – inventory icon suggestion.

## Installation

{% stepper %}
{% step %}
### Place the resource

Put the `ls_wheel_theft` folder into your server `resources` directory.
{% endstep %}

{% step %}
### ESX / QBCore / QBox item setup

* ESX: import `_esx_setup/item.sql` into your items table (or adapt to your schema).
* QBCore: create an item matching `Config.jackStandName` (default: `ls_jackstand_alt`) in your shared items config.
{% endstep %}

{% step %}
### Ensure resource in server.cfg

```cfg
ensure ls_wheel_theft
```
{% endstep %}

{% step %}
### Framework requirement

* ESX server: ensure `es_extended` is started before this resource.
* QBCore server: ensure `qb-core` is started before this resource.
* Optional dispatch resources depending on `Config.dispatch.system` (see [Police / Dispatch Integration](./#police--dispatch-integration)).
{% endstep %}

{% step %}
### Bolt minigame dependency

This script calls:

```lua
exports['ls_bolt_minigame']:BoltMinigame(vehicle, wheelIndex, mount, TaskPlayerGoToWheel, coordsTable)
```

You must install and start the `ls_bolt_minigame` resource (or replace this export with your own system).
{% endstep %}
{% endstepper %}

## Configuration (config.lua)

All config is in `config.lua`. Key sections are summarized here.

### General

```lua
Config.debug = false

Config.command = {
    enabled = true,
    name = 'lift'
}
```

* `debug` – Teleports the player to the mission vehicle when starting a mission.
* `command.enabled` / `command.name` – Enables a chat command (default `/lift`) that will directly lift the nearest vehicle (uses same logic as the jack stand item and triggers `ls_wheel_theft:ResetPlayerState`).

### Framework integration

```lua
Config.esxSettings = {
    enabled = true,
    useNewESXExport = true,
    account = 'bank'
}

Config.qbSettings = {
    enabled = false,
    useNewQBExport = true,
    account = 'bank',
    payInItems = {
        enabled = false,
        itemName = 'cash',
        count = math.random(100, 500)
    }
}
```

* **ESX**
  * `enabled` – set to `true` to use ESX APIs (usable item, bank account money, police job checks).
  * `useNewESXExport` – use `exports['es_extended']:getSharedObject()` or old `esx:getSharedObject` event.
  * `account` – which ESX account receives mission payment.
* **QBCore**
  * `enabled` – set to `true` to use QBCore APIs (usable item, money/items, job checks).
  * `useNewQBExport` – use `exports['qb-core']:GetCoreObject()`.
  * `account` – money account (e.g. `bank`, `cash`) when paying with currency.
  * `payInItems.enabled` – if true, players are paid in `itemName` instead of money.
  * `payInItems.itemName` / `count` – which item and how many to give when `payInItems.enabled` is true.

### Job & jack system

```lua
Config.jackSystem = {
   ['raise'] = {
       everyone = false,
       jobs = {
           'police',
           'ems',
       }
   },
   ['lower'] = {
       everyone = false,
       jobs = {
           'police',
           'ems',
       }
   },
}

Config.job = {
    jobOnly = false,
    jobNames = {
        'thug',
    }
}

Config.jackStandName = 'ls_jackstand_alt'
```

* `jackSystem.raise` / `jackSystem.lower`
  * `everyone = true` – everyone can raise/lower any vehicle.
  * `jobs` – job names that are allowed to raise/lower **any** vehicle.
  * Regardless of this, players can always raise/lower the **current mission target vehicle**.
* `Config.job` controls whether the mission is restricted to certain jobs:
  * `jobOnly = true` – only players whose job is in `jobNames` can do missions.
  * `jobNames` – list of allowed jobs.
* `Config.jackStandName` – item name for the jack stand. ESX/QBCore register this as a usable item that triggers the lift sequence.

### Targeting system (placeholder)

```lua
Config.target = {
    enabled = false,
    system = 'ox-target'
}
```

* Target mode is **not implemented**; the script currently uses key controls and 3D text (`E` / `H`).
* The code includes comments where target integration would go (e.g. in `client.lua`, `BeginWheelLoadingIntoTruck`, `EnableWheelTakeOut`).
* If you implement a target system, respect existing checks (`CanRaiseVehicle`, `CanLowerVehicle`, `JobCheck`, etc.).

### Dispatch / police settings

```lua
Config.dispatch = {
    enabled = false,
    notifyThief = true,
    alertChance = 10,
    system = 'in-built',   -- 'in-built', 'cd-dispatch', 'core-dispatch-old', 'core-dispatch-new', 'ps-dispatch'
    policeCode = '10-31',
    eventName = 'Theft',
    description = 'Suspect is stealing vehicle wheels',
    blip = {
        sprite = 380,
        color = 59,
        scale = 1.0,
        timeout = 60,
        showRadar = true,
    },
}

Config.policeJobNames = {
    'police'
}

Config.blips = {
    policeBlip = {
        sprite = 161,
        color = 47,
        scale = 2.0,
        alpha = 150,
        shortRange = false,
    },
}
```

* `dispatch.enabled` – master switch for dispatch integration.
* `notifyThief` – whether to start vehicle alarm & notify thief in chat/tooltip when police are alerted.
* `alertChance` – percent chance per wheel theft that police will be alerted. Called **up to four times** (once per wheel), so keep this low.
* `system` – which dispatch API to use:
  * `'in-built'` – simple blip + feed notification to police (`ls_wheel_theft:activatePoliceAlarm`).
  * `'cd-dispatch'` – uses `cd_dispatch` export & server event.
  * `'core-dispatch-old'` / `'core-dispatch-new'` – two variants of `core_dispatch` integration.
  * `'ps-dispatch'` – uses `ps-dispatch` export `CustomAlert`.
* `policeJobNames` – job names that count as police for dispatch targeting.
* `blips.policeBlip` – blip style for in‑built police blips.

### Mission vehicles, locations & Peds

```lua
Config.missionLocations = {
    { x = 888.0,   y = -1768.0, z = 29.0, h = 267.3 },
    { x = 1202.9,  y = -1383.0, z = 34.6, h = 359.0 },
    { x = 1268.5,  y = -740.3,  z = 62.5, h = 320.0 },
    { x = -723.4,  y = -913.2,  z = 18.3, h = 270.2 }
}

Config.vehicleModels = {
    'sultanrs', 'cavalcade', 'issi8', 'radi', 'buffalo5',
    'dominator2', 'buffalo4', 'z190', 'asea', 'asterope2', 'rhinehart'
}

Config.missionBlip = {
    showBlip = true,
    blipColor = 29,
    blipIcon = 514,
    blipLabel = 'Tire Theft Mission',
}

Config.missionPeds = {
    ['sale_ped'] = {
        location = { x = 2343.53, y = 3143.0,  z = 48.2,  h = 169.1 },
        wheelDropOff = {
            crateProp = 'prop_crate_09a',
            location = { x = 2345.7, y = 3141.2, z = 47.2 },
        },
        message = 'Sell the tires',
        pedModel = 'g_m_m_mexboss_01',
        duration = 2000,
        price = math.random(300, 500),
        blip = {
            showBlip = true,
            blipColor = 25,
            blipIcon = 431,
            blipLabel = 'Tire Sale',
        },
    },
    ['mission_ped'] = {
        location = { x = 401.3, y = -1927.1, z = 24.8, h = 355.0 },
        pedModel = 'g_m_m_mexboss_01',
        duration = 2000,
        price = math.random(300, 500),
        blip = {
            showBlip = true,
            blipColor = 28,
            blipIcon = 480,
            blipLabel = 'Wheel Theft Missions',
        },
    },
}
```

* `missionLocations` – spawn points for random target vehicles. A random location and model are chosen each mission.
* `vehicleModels` – list of possible target vehicles.
* `missionBlip` – style of the mission target blip.
* `missionPeds.mission_ped` – mission giver NPC: location, model, blip, payout range.
* `missionPeds.sale_ped` – seller NPC: location, drop‑off crate, blip, payout range.

### Pickup truck spawn

```lua
Config.spawnPickupTruck = {
    enabled = true,
    models = { 'bison' },
    truckSpawnCoords = {
        { x = 407.6,  y = -1917.2, z = 25.1, h = 50.6 },
        { x = 405.58, y = -1919.7, z = 24.9, h = 51.0 },
        { x = 403.3,  y = -1922.0, z = 24.7, h = 46.7 },
    }
}
```

* If `enabled`, `StartMission` will call `SpawnTruck()` to give the player a pickup truck.
* Truck models and spawn coordinates are configurable; script ensures a free spot or shows `~r~ No seats available at the moment`.

### Locale & settings

`Locale` holds all user‑facing messages; values can be translated per your language, but **keys must remain unchanged**.\
`Settings.wheelTakeOff` configures the wheel prop model and attach offsets used when the player is carrying a wheel.

## Gameplay Flow

{% stepper %}
{% step %}
### Starting a mission

* A mission giver ped (`Config.missionPeds['mission_ped']`) is spawned on client start (`CreateMissionPed()` in `client/mission.lua`).
* When the player is within \~3 units:
  * If no mission is active: 3D text shows `Press [E] to start mission`.
  * If a mission is active: 3D text shows `Press [E] to cancel mission`.

When starting a mission (`StartMission` in `client/client.lua`), the sequence is:

{% stepper %}
{% step %}
MISSION\_ACTIVATED is set true.
{% endstep %}

{% step %}
Optional: a pickup truck is spawned near the base (`Config.spawnPickupTruck`).
{% endstep %}

{% step %}
A random target vehicle model & mission location are chosen.
{% endstep %}

{% step %}
Coords are blurred using `ModifyCoordinatesWithLimits` to avoid revealing precise location via blip radius.
{% endstep %}

{% step %}
A mission blip and a radius area blip are created for the target vehicle.
{% endstep %}

{% step %}
The target vehicle is spawned and its rims randomized (`SetCustomRims`).
{% endstep %}

{% step %}
Chat tooltip (and optionally console log) shows the vehicle plate number.
{% endstep %}

{% step %}
If the player dies during approach, mission is cancelled and blips are removed.
{% endstep %}
{% endstepper %}
{% endstep %}

{% step %}
### Lifting the vehicle

To steal wheels, the vehicle must be jacked up:

* Via item:
  * ESX: `ESX.RegisterUsableItem(Config.jackStandName, ...)` in `server/esx.lua`.
  * QBCore: `QBCore.Functions.CreateUseableItem(Config.jackStandName, ...)` in `server/qb.lua`.
  * When used, it triggers client event `ls_wheel_theft:LiftVehicle`.
* Via command:
  * If `Config.command.enabled`, the `/lift` (or configured) command calls `RaiseCar()` client‑side and then `ls_wheel_theft:ResetPlayerState` server‑side.

RaiseCar() (in `client/jackstand.lua`) flow:

{% stepper %}
{% step %}
Finds nearest car within 2.0 units.
{% endstep %}

{% step %}
Checks job permissions (`JobCheck` + `CanRaiseVehicle`).
{% endstep %}

{% step %}
Ensures vehicle is a car, stopped, empty driver seat, not already raised.
{% endstep %}

{% step %}
Plays mechanic animation and freezes vehicle.
{% endstep %}

{% step %}
Spawns four jack stand props and positions them beneath wheels.
{% endstep %}

{% step %}
Slowly raises the car (`SetEntityCoordsNoOffset`) by \~0.18 units.
{% endstep %}

{% step %}
Attaches jack stands to car, saves their net IDs into entity state server‑side (`ls_wheel_theft:server:saveJacks`).
{% endstep %}

{% step %}
Marks vehicle as raised via shared state (`Entity(veh).state.IsVehicleRaised = true`).
{% endstep %}
{% endstepper %}
{% endstep %}

{% step %}
### Stealing wheels

Once the car is raised:

* `StartWheelTheft(vehicle)` runs a loop while player is near the vehicle.
* For each wheel:
  * Finds nearest wheel (`FindNearestWheel`).
  * Displays 3D text `Press [E] to start stealing`.
  * On `E` press, chance to notify police (`IsPoliceNotified()` using `Config.dispatch.alertChance`).
  * If police are notified and `notifyThief` is true, starts vehicle alarm and triggers dispatch (`TriggerDispatch`).
  * Starts the bolt minigame (`ls_bolt_minigame` export).
  * On success, hides the wheel using `SetVehicleWheelXOffset` and spawns a wheel prop in player’s hands via `PutWheelInHands`.
  * Calls `BeginWheelLoadingIntoTruck` to allow loading into truck.

When all four wheels have been stolen (`#STORED_WHEELS == 4`):

* Player is instructed via tooltip to go to the wheel seller.
* `EnableSale()` is called and wheel theft loop stops via `StopWheelTheft`.
{% endstep %}

{% step %}
### Loading wheels into truck

With a wheel prop in hands (`WHEEL_PROP` / `HOLDING_WHEEL`):

* `BeginWheelLoadingIntoTruck` scans for a nearby pickup truck (`IsVehicleATruck` uses a preset list of pickup hashes).
* When near the rear of a valid truck, 3D text prompts `Press [E] to store the wheel`.
* On `E` press, the wheel prop is attached into the truck bed (`PutWheelInTruckBed`) at one of four positions and removed from player; `STORED_WHEELS` is updated.

Additionally, `EnableWheelTakeOut()` lets players take wheels back out of the truck using the `H` key while near the truck, as long as there are stored wheels.
{% endstep %}

{% step %}
### Lowering the vehicle

`LowerVehicle()` (in `client/jackstand.lua`):

* Locates nearest raised vehicle.
* If all four wheels are still present and `bypass` is false, shows `Finish the job` tooltip and aborts.
* If the vehicle is raised, gradually lowers it to ground by reversing the raising routine.
* Forces removal of jack stand entities via server event `ls_wheel_theft:server:forceDeleteJackStand`.
* Unfreezes vehicle and sets `IsVehicleRaised` to false in state.
* Called when player completes the theft (both in mission flow and when manually lowering other raised vehicles, subject to job perms).

As part of completing theft on a mission vehicle, `StopWheelTheft` also:

* Prompts `Press [E] to finish stealing` when near vehicle.
* Lowers vehicle, spawns bricks under it (`SpawnBricksUnderVehicle`), and returns the jack stand item via `ls_wheel_theft:RetrieveItem` event.
{% endstep %}

{% step %}
### Selling wheels

When instructed to head to wheel seller:

* `EnableSale()` spawns a seller ped and a crate prop at `Config.missionPeds['sale_ped']`.
* Creates an optional blip for the seller, and can route the player to it if `Config.enableBlipRoute` is true.
* Calls `ContinueSale()` loop:
  * While `saleActive` is true:
    * If the player is holding a wheel near the crate and fewer than 4 wheels are stored, 3D text prompts to `drop off wheel`. On `E`, the wheel is attached into the crate (`DropOffWheel`).
    * When 4 wheels are in the crate, approaching the seller ped shows `Press [E] to complete the sale`.
    * On `E`, `CompleteSale()` is called.

CompleteSale() sequence:

{% stepper %}
{% step %}
Stops the sale loop.
{% endstep %}

{% step %}
Plays money exchange animations between seller and player.
{% endstep %}

{% step %}
Triggers `ls_wheel_theft:Sell` server event with key `sale_ped`.
{% endstep %}

{% step %}
Server side, `AddMoney` pays the player according to their framework:

* ESX: `xPlayer.addAccountMoney(Config.esxSettings.account, selling.price)`.
* QBCore: either adds money to `Config.qbSettings.account` or gives an item.
{% endstep %}

{% step %}
Cleans up ped and wheel entities and removes the seller blip.
{% endstep %}
{% endstepper %}

* Calls `CancelMission()` to reset mission state.
{% endstep %}
{% endstepper %}

## Controls (default)

All keys are defined in `client/client.lua` (`Keys` table). Default controls used:

* `E` – interact (start/cancel mission, jack / unjack operations, start stealing, store wheels, drop wheels, complete sale).
* `H` – take a wheel out of the truck bed (when near truck and wheels are stored).

You can rebind these directly in the code if needed.

## Police / Dispatch Integration

The police integration logic is split:

* **Client** `client/policeAlert.lua` – builds and sends dispatch calls based on `Config.dispatch.system`, shows in‑built notifications & blips.
* **Server** `server/server.lua` – receives theft alerts and either broadcasts built‑in police alarms or triggers dispatch exports.

### Flow

1. During a wheel theft, when the player uses `E` to start unbolting a wheel, `IsPoliceNotified()` checks the random chance.
2. If success and `Config.dispatch.enabled`, `TriggerDispatch` sends a server event `ls_wheel_theft:PoliceAlert` with theft coordinates.
3. Server decodes coords and, if dispatch is enabled:
   * For `in-built`, loops through all players, checks `IsPolice` (framework‑specific job check), and triggers client event `ls_wheel_theft:activatePoliceAlarm`.
   * For other systems, forwards the alert to the appropriate client events / exports (ps‑dispatch, cd‑dispatch, core‑dispatch).
4. On police clients, `ls_wheel_theft:activatePoliceAlarm`:
   * Creates a `PoliceAlarm` blip at the theft site.
   * Uses `DisplayAlert` to post a notification with street name.
   * Clears blips after a delay.

Ensure the chosen dispatch resource is installed and configured if `Config.dispatch.enabled` is `true` and `system` is not `'in-built'`.

## ESX Integration Details

* Client: `client/framework_functions/esx.lua`
  * Obtains shared ESX object (new/old pattern).
  * Waits for player job data then sets `PLAYER_JOB`.
  * Updates `PLAYER_JOB` on `esx:setJob` events.
* Server: `server/esx.lua`
  * Registers usable item `Config.jackStandName` – triggers `ls_wheel_theft:LiftVehicle` and removes one item.
  * `IsPolice(player)` – checks job name against `Config.policeJobNames`.
  * `RetrieveItem(source, item)` – gives the jack stand back after mission.
  * `AddMoney(player, amount)` – pays into specified ESX account.
  * `UseItem(source)` – helper to remove one jack stand from inventory on use.

## QBCore/QBox Integration Details

* Client: `client/framework_functions/qb.lua`
  * Gets `QBCore` object if enabled.
  * Reads `PLAYER_JOB` from `QBCore.Functions.GetPlayerData`.
  * Updates `PLAYER_JOB` on `QBCore:Client:OnPlayerLoaded` and `QBCore:Client:OnJobUpdate`.
* Server: `server/qb.lua`
  * Registers usable item `Config.jackStandName` → triggers `ls_wheel_theft:LiftVehicle` and removes one item.
  * `IsPolice(player)` – checks QBCore player job against `Config.policeJobNames`.
  * `RetrieveItem(source, itemId, count)` – adds items to player inventory.
  * `AddMoney(player, amount)` – either gives items or money depending on `Config.qbSettings.payInItems`.
  * `RemovePlayerItem(player, item, amount)` / `UseItem(source)` – wrappers for removing items.

## Events Reference

### Client Events

* `ls_wheel_theft:LiftVehicle`\
  Called by server when player uses jack stand item. Starts `RaiseCar()` and then asks server to reset mission state.
* `ls_wheel_theft:LowerVehicle`\
  Lowers nearest raised vehicle via `LowerVehicle()`.
* `ls_wheel_theft:TriggerDispatchMessage`\
  Used when `Config.dispatch.system` is not `'in-built'` to forward dispatch calls to `ps-dispatch`, `cd-dispatch`, or `core_dispach`.
* `ls_wheel_theft:activatePoliceAlarm`\
  In‑built dispatch – shows blip + notification to police jobs.

### Server Events

* `ls_wheel_theft:Sell` (`sellingKey`)\
  Handles final payment when sale is completed (`sellingKey` is typically `'sale_ped'`). Calls framework‑specific `AddMoney`.
* `ls_wheel_theft:server:setIsRaised` (`netId`, `raised`)\
  Sets `Entity(veh).state.IsVehicleRaised` shared state for a vehicle.
* `ls_wheel_theft:PoliceAlert` (`locationCoords`)\
  Main entry for theft alerts; decodes coords and triggers correct police/dispatch flow.
* `ls_wheel_theft:RetrieveItem` (`itemName`)\
  Returns jack stand item to player at end of mission.
* `ls_wheel_theft:ResetPlayerState` (`netId`)\
  After a delay, resets `Player(_source).state.WheelTheftMission` to false; used when lifting car via item/command.
* `ls_wheel_theft:server:forceDeleteJackStand` (`state`)\
  Converts jack stand net ID to entity and deletes it when lowering vehicle.
* `ls_wheel_theft:server:saveJacks` (`netId`, `jack1`..`jack4`)\
  Persists jack stand net IDs into vehicle state so they can be cleaned later.
