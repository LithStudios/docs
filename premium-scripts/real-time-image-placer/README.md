---
description: >-
  A comprehensive image placement and viewing tool script that allows
  administrators and players to place, edit, and view custom images in the game
  world with advanced positioning and customization opti
---

# Real-time image placer

## Features

* Interactive image placement system
* Gif support
* Real-time position and rotation adjustment
* Scale customization with drag-to-adjust
* Texture streaming and loading
* Persistent image storage and database integration
* Admin permission system
* Player permission settings for viewing

## Installation

{% stepper %}
{% step %}
Place `ls_image_placer` in your resources folder
{% endstep %}

{% step %}
Configure the script (see Configuration section)
{% endstep %}

{% step %}
Add to server.cfg:

{% code title="server.cfg" %}
```cfg
ensure ls_image_placer
```
{% endcode %}
{% endstep %}

{% step %}
Restart your server
{% endstep %}
{% endstepper %}

## Dependencies

* **Required:** None (standalone)
* **Recommended:**
  * Framework (ESX/QBCore) for permission system
  * Database system for persistence
  * Admin system for access control

## Performance

* **Optimized rendering** - LOD-based system
* **Efficient storage** - Compressed images
* **Smart caching** - Limited image cache
* **Idle:** 0.00ms
* **Placement mode:** 0.02-0.03ms
* **Rendering active:** 0.01ms per image

## Support

For issues or questions:

* Enable debug mode first
* Check console for errors
* Verify file structure
* Contact Lith Studios support
