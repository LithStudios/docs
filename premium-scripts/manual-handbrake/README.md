---
description: >-
  Handbrake script that enables realistic manual handbrake mechanics with drift
  capabilities, realistic physics, and enhanced driving dynamics.
---

# Manual handbrake

## Features

* Manual handbrake control with realistic physics
* Configurable rolling angle and speed multiplier
* Realistic vehicle rolling when not engaged
* Custom sound effects
* Configurable exempt vehicle classes and models

## Installation

{% stepper %}
{% step %}
### Place resource and configure

* Place `ls_handbrake` in your resources folder
* Configure the script (see Configuration section)
{% endstep %}

{% step %}
### Add to server config

Add to `server.cfg`:

```cfg
ensure ls_handbrake
```
{% endstep %}

{% step %}
### Restart

* Restart your server
{% endstep %}
{% endstepper %}

## Dependencies

* **Required:** None (standalone)

## Support

For issues or questions:

* Enable debug mode first
* Check console for errors
* Review vehicle configuration
* Contact Lith Studios support
