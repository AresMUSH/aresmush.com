---
title: Start the Game
description: 
layout: page
tags:
- manage
- restart
---

If the game is ever stopped, you'll need to start it. 

1. Log into your [Server Shell](/tutorials/manage/server-shell.html) with the ares user.
2. Type `cd aresmush`.
3. Type `bin/startares`.

{% note %}
Never try to start the game with the root user.
{% endnote %}

If the game is already running and you want to restart it:

1. Log into your [Server Shell](/tutorials/manage/server-shell.html) with the ares user.
2. [Shut Down the Game](/tutorials/manage/shutdown.html) first.
3. Wait about 10 seconds.  This ensures that everything has a chance to shut down fully.
4. Type `cd aresmush`.
5. Type `bin/startares`.

Your game should also automatically restart when the server is rebooted.  If that doesn't happen for some reason, see [Auto-Restart After Server Reboot](/tutorials/manage/restart-after-reboot.html).

## Debug Mode

Both the game and portal can be started in [Debug Mode](/tutorials/code/debug-mode.html).  This is good for temporary debugging, but the game only stays running as long as you're logged in.  It's not a permanent solution.
