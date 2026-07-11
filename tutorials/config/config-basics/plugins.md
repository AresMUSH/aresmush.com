---
title: Essential Config - Selecting Plugins
description: 
layout: tutorial
nextstep: text
prevstep: game-dir
tutorialIndex: tutorials/config/config-basics
essentialConfigTutorial: true
tutorialName: Essential Config
tags:
- config
---

A few Ares plugins are designed to be optional so you can easily disable them if you don't need them for your game.

1. Go to Admin -> Setup in the web portal.
2. Select "Enable or Disable Plugins".
2. Check or uncheck plugins to enable/disable them.

{% include pretty_image.html file='web-portal/plugins.png' %}

For example:

* If your game doesn't use military ranks, you'll want to disable the Ranks plugin.
* If you plan to use a different skills/chargen system, you can disable FS3 skills and combat.
* If your game is set on a spaceship or you just hate coded weather, you can turn off the weather system.

{% tip %} 
If you disable the chargen system, you'll have to replace it with your own custom chargen, or else manually assign the approved role to approved characters (using `role/add <character>=approved`). Many commands are locked to only approved characters.
{% endtip %}

If a plugin is not listed on this screen, that means it cannot be disabled without custom code changes. For more information about this, and to learn what happens behind-the-scenes when you disable a plugin, see [Enabling and Disabling Plugins](/tutorials/config/plugins.html).

## Navbar

If you disable plugins, particularly FS3, you will also want to review your [Web Portal menu](/tutorials/config/website.html#navbar) to remove any navigation items related to that system.