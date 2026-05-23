---
description: >-
  This guide will help you get started with Lith Studios scripts on your FiveM
  server.
icon: flag-checkered
---

# Getting started

## Prerequisites

Before installing any Lith Studios scripts, ensure you have:

* FiveM Server - A working FiveM server (latest stable version)
* Framework - ESX or QBCore or QBox installed (for most scripts)
* Database - database server running
* Basic Knowledge - Understanding of FiveM server structure and Lua scripting

## Installation Process

### General Installation Steps

{% stepper %}
{% step %}
### Download the Script

* Obtain the script from Lith Studios
* Extract the archive to a temporary location
{% endstep %}

{% step %}
### (Optional) Create a \[lith] folder

Create a folder name `[lith]` for easy storage to all our scripts
{% endstep %}

{% step %}
### Place in Resources Folder

```bash
/resources/[lith]/script_name/
```
{% endstep %}

{% step %}
### Install and configure kq\_link (if applicable)

Newer scripts use [kq\_link](https://github.com/Kuzkay/kq_link). Wheter you need to install kq\_link is in our package description on our website. To configure kq\_link:

* Open `config.lua` or similar configuration files
* Set your framework (ESX or QBCore)
* Adjust settings to match your server need
{% endstep %}

{% step %}
### Database Setup (if required)

* Import any `.sql` files provided
* Configure SQL driver in config (if script doesn't use kq\_link)
* Test database connection
{% endstep %}

{% step %}
### Add to server.cfg

```cfg
ensure script_name
```
{% endstep %}

{% step %}
### Start/Restart Server

* Start your server or use `refresh` and `ensure script_name`
{% endstep %}
{% endstepper %}

### Script-Specific Requirements

Some scripts have special requirements:

{% hint style="warning" %}
ls\_wheelspacers need ls\_bolt\_minigame to function
{% endhint %}

### Scripts using kq\_link

* ls\_locker\_theft
* ls\_pickpocketing
* ls\_snatch
* ls\_handbrake
* ls\_props
* ls\_wheelspacers
* ls\_image\_placer
* ls\_brake\_cutting

## Testing

{% stepper %}
{% step %}
### Test in Development

* Set up a test server with your configuration
* Test all features thoroughly
* Check for console errors
{% endstep %}

{% step %}
### Performance Check

* Monitor server performance (ms)
* Check for any lag or stuttering
* Optimize render distances if needed
{% endstep %}

{% step %}
### Player Testing

* Have players test the script
* Gather feedback on gameplay
* Make adjustments as needed
{% endstep %}
{% endstepper %}

## Common Issues

### Script Not Starting

* Check `server.cfg` has `ensure script_name`
* Verify all dependencies are installed
* Check console for error messages
* Ensure proper folder structure

### Database Errors

* Verify SQL driver is correct in config
* Check database credentials
* Ensure tables are created
* Test database connection

### Framework Issues

* Confirm framework is running
* Check framework version compatibility
* Verify framework export settings
