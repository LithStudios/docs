---
description: >-
  An expansive heist script featuring multi-stage robberies on Cartel Island
  with complex objectives, NPC interactions, and high-stakes rewards.
hidden: true
---

# Cartel heist

## Features

* Multi-stage heist with progressive objectives
* Dynamic NPC patrol and engagement systems
* Complex lock-picking and hacking mechanics
* Cooperative gameplay support for teams
* Large-scale loot distribution
* Police response and escape mechanics
* Vehicle requirements and parking systems
* Hidden passage and alternative routes
* Loot bag system with weight/capacity
* Real-time timer and progress tracking
* Stealth and combat mechanics
* Comprehensive failure conditions

## Installation

{% stepper %}
{% step %}
### Install resource

Place `ls_cartel_heist` in your resources folder.
{% endstep %}

{% step %}
### Configure

Configure the script (see Configuration section).
{% endstep %}

{% step %}
### Add to server.cfg

```cfg
ensure ls_cartel_heist
```
{% endstep %}

{% step %}
### Restart

Restart your server.
{% endstep %}
{% endstepper %}

## Dependencies

* **Required:**
  * None (standalone)
* **Recommended:**
  * Framework (ESX/QBCore) for player data
  * Dispatch system for police alerts
  * Vehicle system for requirements
  * Inventory system for loot handling

## How It Works

### Heist Flow

{% stepper %}
{% step %}
### Setup

* Players gather required vehicles
* Travel to Cartel Island
* Approach starting location
{% endstep %}

{% step %}
### Stage 1: Infiltration

* Avoid or neutralize guards at gate
* Maintain stealth meter
* Reach vault entrance without alarming guards
{% endstep %}

{% step %}
### Stage 2: Vault Access

* Complete hacking minigame
* Open main vault door
* Time pressure increases difficulty
{% endstep %}

{% step %}
### Stage 3: Looting

* Collect loot bags from vault
* Avoid detection during collection
* Fill inventory with valuable items
* Drop items if necessary
{% endstep %}

{% step %}
### Stage 4: Escape

* Travel to extraction point
* Evade police (if alerted)
* Reach destination
* Mission complete
{% endstep %}
{% endstepper %}

## Performance

* **Optimized NPC systems** - Limited patrol radius
* **Efficient objective tracking** - Minimal callbacks
* **Smart loot management** - Weight-based system
* **Idle:** 0.01ms
* **Active:** 0.05-0.10ms
* **Multiple NPCs:** 0.15ms

## Support

For issues or questions:

* Enable debug mode first
* Check console for errors
* Review stage configuration
* Contact Lith Studios support
