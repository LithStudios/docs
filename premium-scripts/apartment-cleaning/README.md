---
description: >-
  A comprehensive job script that allows players to earn money through property
  cleaning assignments with progressive difficulty and performance-based
  rewards.
---

# Apartment cleaning

## Features

* Multiple cleaning locations
* Progressive difficulty levels with scaled rewards
* Police avoidance mechanics
* Customizable location and reward settings
* Multi-language support
* Comprehensive performance metrics

## Installation

{% stepper %}
{% step %}
Place `ls_cleaning` in your resources folder
{% endstep %}

{% step %}
Configure the script (see Configuration section)
{% endstep %}

{% step %}
Add to server.cfg:

```cfg
ensure ls_cleaning
```
{% endstep %}

{% step %}
Restart your server
{% endstep %}
{% endstepper %}

## Dependencies

* **Required:**
  * None (standalone)
* **Recommended:**
  * Framework (ESX/QBCore) for job management
  * Banking system for pay deposits
  * Vehicle system for job assignments

## Performance

* **Optimized area tracking** - Only checks nearby areas
* **Smart payment calculation** - Minimal overhead
* **Idle:** 0.00ms
* **Job active:** 0.01-0.02ms
* **3D text active: \~**&#x30;.10ms

## Support

For issues or questions:

* Enable debug mode first
* Check console for errors
* Review location configuration
* Contact Lith Studios support
