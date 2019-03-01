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

{% include note.html content="You should use the 'ares' user for everything from now on, reserving the root user for rare server admin operations requiring root access.  The `setup_server` script should have created the ares user for you automatically and printed the password.  You should be able to scroll back if you missed it." %}

1. Log into your [Server Shell](/tutorials/install/server-shell.html) with the **'ares' user**.

2. Copy/paste the following commands into the shell to run them.

        curl https://raw.githubusercontent.com/aresmush/aresmush/master/bin/install > install
        
        chmod +x install
        
        ./install
        
        export NVM_DIR="$HOME/.nvm"
        [ -s "$NVM_DIR/nvm.sh" ] && \. "$NVM_DIR/nvm.sh" 

3.  Enter your ares password when prompted.

4.  Enter the information about your game, as explained below.

This will take several minutes.  There will be a lot of spam, but eventually it will say it's done.

{% include note.html content="If you already have a GitHub fork, you can pass the HTTPS clone urls to the install script: `./install &lt;game code clone URL> &lt;Web Portal clone URL>`   If you don't have a GitHub fork (or don't know what that even means) then just leave off those URLs." %}

## Game Settings

These are the basic settings you'll need to enter:

* **Database URL** - Where the database server lives.  If you're using the standard setup scripts, it's `127.0.0.1:6379`
* **Server Hostname** - The the game's [host name](/tutorials/install/getting-a-hostname.html) or IP Address.  Use the actual IP or host name, not just "localhost".
* **Server Telnet Port** - See ports, below.
* **Server Websocket Port** - See ports, below.
* **Server Web Portal Port** - See ports, below.
* **MUSH Name** - Name your game.
* **MUSH Description** - A short blurb about your game (optional).
* **Category** - Pick which category best describes your MUSH for the Ares games folder.
* **GitHub Email** - See GitHub, below.
* **GitHub Name** - See GitHub, below.

### GitHub

AresMUSH is stored in GitHub, a popular software version control system.  Sometimes you need to interact with GitHub to retrieve Ares code updates.  For this, GitHub needs to be configured with an email and a name.  

{% include note.html content="If you do not plan on using GitHub for version control, you can make these dummy values - any email (even a fake one) and name will do." %}

* Email - If you plan to use GitHub to store [your own code changes](/tutorials/code/git.html), then you should use the email address associated with your GitHub account.  Some people even create a special GitHub account solely for their game work.  
* Name - The name is just a record of who made code changes.

### Ports

Whereas the old MUSH servers you might be useful have only one port (mush.somewhere.com port 1234) Ares actually uses several.  You can use any port that isn't already in use.  On a VPS server, ports greater than **1024** are typically open.

The **Telnet Port** is the general one that regular MU clients connect to.  (default 4201)

The **Websocket Port** and **Engine API Port** are behind-the-scenes ports that the Ares Web Portal uses to communicate with the game. (default 4202 and 4203)

The **Web Portal Port** is where your Web Portal is running. (default 80)  '80' works if the Web Portal is the only website running on the server.  Otherwise you'll need to pick a custom port and access the Web Portal through a URL like http://mush.somewhere.com:8081.

{% include note.html content=" Be aware that running the Web Portal on a port other than '80' may prevent some players from accessing it through their work/school firewalls." %}