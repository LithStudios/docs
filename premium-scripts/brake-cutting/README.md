---
description: >-
  A sophisticated vehicle sabotage script that allows players to cut vehicle
  brakes with realistic physics effects and consequential gameplay mechanics.
---

# Brake cutting

## Features

* Interactive brake cutting minigame with realistic mechanics
* Physics-based brake failure system
* Configurable failure distances and triggers
* Vehicle detection and selection system
* Police dispatch integration
* Multi-language support
* Advanced debug system

## Installation

1. Place `ls_brake_cutting` in your resources folder
2. Configure the script (see Configuration section)
3. Add to server.cfg:

```cfg
ensure ls_brake_cutting
```

4. In F8 console type `refresh` followed by `ensure ls_bolt_minigame`

## Dependencies

* Required:
  * None (standalone)
* Recommended:
  * Framework (ESX/QBCore) for player tracking
  * Dispatch system for crime alerts
  * Vehicle system for vehicle data

## Performance

* Efficient minigame - Lightweight action system
* Idle: 0.00ms
* Minigame active: 0.03ms

## Support

For issues or questions:

* Enable debug mode first
* Check console for errors
* Review vehicle configuration
* Contact Lith Studios support
