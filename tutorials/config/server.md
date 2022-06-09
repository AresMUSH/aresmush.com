---
title: Configuring the Server
layout: page
tags:
- config
---

Your server host and port information are set up during installation.  If they ever change, you'll need to update the configuration.

For more info on server configuration options, see [Installing the Game](/tutorials/install/install-game.html).

To configure the server:

1. Select Admin -> Setup
2. Edit `server.yml`.
4. Shutdown and restart the game. (See the tutorials at [aresmush.com](http://www.aresmush.com) if you need help doing this.)

{% note %} 
Server setting changes will not take effect until the game is restarted.
{% endnote %}

{% include toc.html %}

## Advanced Server Options

These advanced server options will not be needed by every game.

### HTTPS Web Portal

See [Setting up HTTPS]({{site.baseurl}}/tutorials/install/https.html).

### bind_address

When hosting a game on a host with separate public/private IP addresses (commonly found with AWS) you'll need to tell the server to start up on the private IP.  Do this by setting the `bind_address` config option to the private IP.

{% note %} 
Remember to restart the game engine after changing this setting.
{% endnote %}

