---
title: Rebooting the Server
description: 
layout: page
tags:
- reboot
- upgrade
---

Sometimes your server will tell you it needs to be restarted.  Usually this happens after it has auto-installed security updates.  You might see this notice when you log into the server shell, or when you view the Ares jobs list.

In the server shell:

> `*** System restart required ***`

In the game:

> Your operating system is indicating that your server needs to be rebooted - probably to finish installing automatic updates.  Please restart the server (not just the game) as soon as you can.  You may encounter performance or memory issues until this is done.

{% note %} 
It is highly recommended that you reboot your system as soon as possible when you see this message.  Not only will this get you the necessary security updates faster, but it will avoid lag and other performance issues.
{% endnote %}

## How to Reboot

1. Shut down the game, either using the `shutdown` command or the Admin->Manage->Shutdown button on the Web Portal.
2. Log into the [Server Shell](/tutorials/manage/server-shell.html).
3. Type `sudo reboot`.  (On older linux systems you may need to do `sudo shutdown -r now`.)
4. Your server shell will be disconnected. This is normal, since the server is rebooting. Keep trying to reconnect every few minutes, and you will eventually be able to.
5. Your game should restart automatically after the server reboots. 

{% warning %}
It usually takes a few minutes, sometimes up to 30, for the OS to install the updates after a reboot. This is similar to what happens when you get the blue screen saying "Installing Windows updates. Don't turn off your computer." when you update your PC. You just can't see the server screen. Just be patient.
{% endwarning %}

If your game doesn't restart automatically after the restart, there's probably some other error. See [troubleshooting](/tutorials/code/troubleshooting.html) or ask for help.