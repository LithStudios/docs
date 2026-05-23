---
description: >-
  An interactive prop viewing script that allows players and admins to spawn,
  position, and interact with custom props and objects throughout the game world
  with comprehensive configuration and manageme
---

# Viewable props

## Features

* NUI-based image viewing
* Configurable view permissions based on job
* Target support



## Installation

{% stepper %}
{% step %}
### Place resource

Place `ls_props` in your resources folder
{% endstep %}

{% step %}
### Configure

Configure the script (see Configuration section)
{% endstep %}

{% step %}
### Add to server.cfg

```cfg
ensure ls_props
```
{% endstep %}

{% step %}
### Restart

Restart your server
{% endstep %}
{% endstepper %}

## Dependencies

* **Required:**
  * None (standalone)
* **Recommended:**
  * Framework (ESX/QBCore) for permission system
  * Database system for persistence
  * Admin system for access control

## Performance

* **Optimized rendering** - LOD-based system
* **Efficient storage** - Compressed data
* **Smart loading** - Distance-based loading
* **Idle:** 0.00ms
* **Spawning:** 0.02-0.03ms
* **Rendering:** 0.01ms per prop

## Support

For issues or questions:

* Enable debug mode first
* Check console for errors
* Verify prop models exist
* Contact Lith Studios support
