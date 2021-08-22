---
title: Install the Game
description: 
layout: tutorial
installTutorial: true
tutorialName: Installing AresMUSH
tutorialIndex: tutorials/install
prevstep: setup-server
nextstep: next-steps
tags:
- install
- config
---

Next we'll configure some basic information about your game.  These settings determine how you connect to the game.  When your game opens, the MU* description, website, etc. will appear in the AresMUSH games folder.

{% include custom_install_warning.md %}

{% note %} 
You should use the 'ares' user for everything from now on, reserving the root user for rare server admin operations requiring root access.  The `setup_server` script should have created the ares user for you automatically and printed the password.  You should be able to scroll back if you missed it.
{% endnote %}


1. Log into your [Server Shell](/tutorials/install/server-shell.html) with the **'ares' user**.

{:start="2"}
2. Copy/paste the following commands into the shell to run them **one by one**.  Wait until one command has completed before pasting the next command.

        curl https://raw.githubusercontent.com/aresmush/aresmush/master/bin/install > install
        
        chmod +x install
        
        ./install
        
        export NVM_DIR="$HOME/.nvm"
        [ -s "$NVM_DIR/nvm.sh" ] && \. "$NVM_DIR/nvm.sh" 

{:start="3"}
3.  Enter your ares password when prompted.

4.  Enter the information about your game, as explained below.

This will take several minutes.  There will be a lot of spam, but eventually it will say it's done.

## Game Settings

These are the basic settings you'll need to enter:

* **Server Hostname** - The the game's [host name](/tutorials/install/getting-a-hostname.html), like yourmush.aresmush.com or your custom domain.  If you don't have a domain name, you can just use your server's IP address.
* **Server Telnet Port** - See ports, below.
* **Server Websocket Port** - See ports, below.
* **Server Web Portal Port** - See ports, below.
* **MUSH Name** - Name your game.
* **Database URL** - See ports, below.

You can edit the MUSH name, description and other game directory details later in the [Game Directory settings](/tutorials/config/game.html).

### Ports

Whereas the old MUSH servers you might be used to have only one port (mush.somewhere.com port 1234) Ares actually uses several.  You can use any port that isn't already in use.  On a VPS server, ports greater than **1024** are typically open.

The **Telnet Port** is the general one that regular MU clients connect to.  (default 4201)

The **Websocket Port** and **Engine API Port** are behind-the-scenes ports that the Ares Web Portal uses to communicate with the game. (default 4202 and 4203)

The **Web Portal Port** is where your Web Portal is running. (default 80)  '80' works if the Web Portal is the only website running on the server.  Otherwise you'll need to pick a custom port and access the Web Portal through a URL like http://mush.somewhere.com:8081.

The **Database URL** is the server/port for connecting to the database.  If you're using the supported environment, it's `127.0.0.1:6379`.

{% note %} 
 Be aware that running the Web Portal on a port other than '80' may prevent some players from accessing it through their work/school firewalls.
{% endnote %}