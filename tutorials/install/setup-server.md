---
title: Setup the Server
description: 
layout: tutorial
installTutorial: true
tutorialName: Installing AresMUSH
tutorialIndex: tutorials/install
prevstep: server-shell
nextstep: install-game
tags:
- install
- code
---

Ares needs a few things installed on the server.  For your convenience, a set of install scripts help to automate the necessary setup.

{% include custom_install_warning.md %}

1. Log into your [Server Shell](/tutorials/install/server-shell.html).

2. Copy/paste the following commands to run them **one by one**.  Wait until one command has completed before pasting the next command.  
   
        curl https://raw.githubusercontent.com/aresmush/aresmush/master/bin/setup_server > setup_server  
    
        chmod +x setup_server
    
        sudo ./setup_server

3. When it asks you to accept unattended upgrades, say yes and accept the default options.  On Linode, you'll have to say 'yes' to a few packages it wants to overwrite too.  

This will take several minutes.  There will be a lot of spam, but eventually it will say it's done.  If any weird errors happen, you can [ask for help](/feedback.html).

> The script will create an 'ares' user and print the temporary password.  This should appear at the end of the giant spam.  Keep this in a safe place; you will need it in a moment.
