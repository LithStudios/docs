# Postal locker theft

An advanced locker theft script allowing players to steal items from secure storage locations with sophisticated lock-picking mechanics and risk management

## Features

* Interactive lock-picking minigame with time pressure
* Multiple lock difficulty levels
* Configurable locker locations and contents
* Security system with alarms and police dispatch
* Loot randomization and rarity tiers
* Cooldown per locker to prevent spam
* Progress tracking for multi-stage lockers
* Silent vs. alarm-triggered theft modes
* Blip system for locker locations
* Multi-language support
* Comprehensive debug logging

## Installation

1. Place `ls_locker_theft` in your resources folder
2. Configure the script (see Configuration section)
3. Add to server.cfg:

```cfg
ensure ls_locker_theft
```

4. Restart your server

## Dependencies

* Required:
  * None (standalone)
* Recommended:
  * Framework (ESX/QBCore) for inventory integration
  * Dispatch system for alarm triggers
  * Alarm system integration

## Performance

* Optimized locker scanning - Only checks nearby locations
* Efficient minigame - Lightweight rotation system
* Smart cooldown management - Minimal memory overhead
* Idle: 0.00ms
* Active: 0.02-0.03ms
* Minigame active: 0.04ms

## Support

For issues or questions:

* Enable debug mode first
* Check console for errors
* Review locker configuration
* Contact Lith Studios support
