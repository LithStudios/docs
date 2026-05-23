# Bolt minigame

An interactive bolt-fastening minigame script for vehicle maintenance, construction work, and mechanical tasks with realistic physics and difficulty progression.

## Features

* Interactive bolt-tightening minigame system
* Rotational physics and realistic torque mechanics
* Success/failure consequences
* Reusable minigame template for various tasks
* Integration with job systems
* Debug mode and logging
* Multi-language support

## Installation

{% stepper %}
{% step %}
Place `ls_bolt_minigame` in your resources folder.
{% endstep %}

{% step %}
Configure the script (see Configuration section).
{% endstep %}

{% step %}
Add to server.cfg:

{% code title="server.cfg" %}
```cfg
ensure ls_bolt_minigame
```
{% endcode %}
{% endstep %}

{% step %}
In F8 console type `refresh` followed by `ensure ls_bolt_minigame`
{% endstep %}
{% endstepper %}

## Dependencies

* **Required:** None (standalone)
