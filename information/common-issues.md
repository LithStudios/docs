---
description: >-
  This comprehensive guide covers common problems across all Lith Studios
  scripts with proven solutions.
icon: circle-info
---

# Common issues

## Script Errors on Startup

{% hint style="info" %}
Most of errors on startup are caused by FileZilla. Use WinSCP instead.
{% endhint %}

{% hint style="danger" %}
**Error parsing script / Failed to load script** _**Error parsing script @...lua in resource ...: @...lua:1: syntax error near '<\1>'**_
{% endhint %}

Your server artifacts are likely outdated. Update your server. ([https://www.youtube.com/watch?v=aXCgN07a-yY](https://www.youtube.com/watch?v=aXCgN07a-yY)). Do **not** use FileZilla. Use WinSCP for transfering resource files.

{% hint style="danger" %}
**You lack the required entitlement to use \<resource>**
{% endhint %}

Try restarting your server and make sure your server license key is correct. If you bought the resource on the wrong account, you can transfer it to another account on [CFX portal](https://portal.cfx.re/).

{% hint style="danger" %}
**Failed to verify protected resource**
{% endhint %}

Files were possibly corrupted during transfer. Ensure hidden files are copied; the .fxap file in a protected resource must be included. Some FTP programs skip these files.

## **Database Issues**

{% hint style="danger" %}
**Table 'table\_name" doesn't exist**
{% endhint %}

Some scripts come with a `.sql` file, make sure to run this file in your database manager, like HeidiSQL. After running the `.sql` file, the database table will be added to your database. Make sure to restart the server for the table to be loaded in.
