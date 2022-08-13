---
title: Understanding Game Ports
description: 
layout: tutorial
installTutorial: true
tutorialName: Installing AresMUSH
tutorialIndex: tutorials/install
prevstep: getting-a-hostname
nextstep: https
tags:
- install
- config
---

Whereas the old MUSH servers you might be used to have only one **port** (mush.somewhere.com port 4201) Ares actually uses several.  You can use any port that isn't already in use.  Ports greater than **1024** are typically open, but it will depend on your specific server configuration.

{% note %}
In Easy Mode or OnClick installs, you only need to select the telnet port; the others are automatically assigned.
{% endnote %}

|Port | Default | Description |
| ---- |
| Telnet | 4201 | How players connect using a MU client, same as Penn/Tiny/Rhost. |
| Web Portal | 80 | How players connect using a web browser. 80 is the default HTTP port, so players can just use your hostname directly (like `http://yourmush.com`). If you use a custom port, everyone will need to specify it in the web browser (like `http://yourmush.com:8081`), and players may have trouble accessing the web portal through work/school firewalls.|
| Websocket | 4202 | Behind-the-scenes port for live updates between the game and web portal. |
| Engine API | 4203 | Behind-the-scenes port for requests from the web portal to the game. |