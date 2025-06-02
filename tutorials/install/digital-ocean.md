---
title: DigitalOcean Self-Install
description: 
layout: tutorial
installTutorial: true
tutorialName: Installing AresMUSH
tutorialIndex: tutorials/install
prevstep: index
nextstep: getting-a-hostname
tags:
- install
- hosting
---

This article will walk you step-by-step through the process of setting up your game using [DigitalOcean](http://www.digitalocean.com/?refcode=5c07173bc1f2).

{% include toc.html %}

## How It Works

Here's how it works in brief (full details follow in the rest of the article):

1. You create a DigitalOcean droplet to host your game.
2. You install the necessary software.
3. You configure your game.

These steps are described in more detail in the next few sections.

> **Full Disclosure:** I get a referral bonus from DigitalOcean if you sign up using [this referral link](http://www.digitalocean.com/?refcode=5c07173bc1f2), but you also get a starter credit. The referral bonus helps keep the doors at [AresCentral](/arescentral.html) open.

## Create a Droplet

Create a [DigitalOcean](http://www.digitalocean.com/?refcode=5c07173bc1f2) account if you don't already have one. From your account dashboard, select **Create -> Droplet**.  

1. Select the Ubuntu distribution image.  (Ares' standard install is 22.04.)  Just use the regular Ubuntu, not any other image.
{% include pretty_image.html file='/install-ares/install-droplet-1.png' %}

{:start="2"}

2. Select a "Shared CPU" and "Basic" droplet, then choose a size. The 2GB/1CPU droplet will suit most Ares games. Giant games may need more RAM, but you can always upgrade later. Below 2GB is not supported.

{% include pretty_image.html file='/install-ares/install-droplet-2.png' %}

{:start="3"}

3. Don't add block storage.
4. Select a region. New York is a good choice unless your players are predominately from outside the US.
5. Select an SSH key for logging in (if you don't know what that is, just select the password option) and any other options desired.
6. Do **NOT** enable IPv6; Ares does not support dual IP versions, and many PCs can still only access v4.

## Connect to the Server Shell

To connect to your game, you will use the IP address/host name and a tool that supports Secure Shell (SSH) connections:

* Windows PowerShell
* Mac Terminal
* PuTTY, available for [Windows](http://www.putty.org/) and [Mac](https://www.ssh.com/ssh/putty/mac/)
* Any other SSH tool
* DigitalOcean console (available through your DigitalOcean account, but very rudimentary)

For more detailed help with the server shell, see [Connecting to the Server Shell]({{site.baseurl}}/tutorials/manage/server-shell.html).

{% note %}
The very first time you connect, you will use the "root" user. If you set up a SSH key for your droplet, you will use that in place of the password. Otherwise a password will be emailed to you. The server setup will create an "ares" user, which is what you'll use from then on.
{% endnote %}

## Set Up the Server

Once your droplet is created, you will need to install the programs Ares requires (Ruby, the Redis Database, the Nginx web server, etc.).  For your convenience, a set of install scripts automate the necessary setup.

1. Log into your [Server Shell](/tutorials/install/server-shell.html) using the **root** user.

2. Copy/paste the following commands to run them **one by one**.  Wait until one command has completed before pasting the next command.  
   
        curl https://raw.githubusercontent.com/aresmush/aresmush/master/bin/setup_server > setup_server  
    
        chmod +x setup_server
    
        sudo ./setup_server

This will take several minutes.  There will be a lot of spam, but eventually it will say it's done. 

> The script will create an 'ares' user and print the temporary password.  This should appear at the end of the giant spam.  Keep this in a safe place; you will need it in a moment.

## Install the Game

Now we can install your Ares game on the server.

1. Log into your [Server Shell](/tutorials/install/server-shell.html), but this time use the **ares** user.

{% warning %} 
You should use the 'ares' user for everything from now on, tucking 'root' away for safekeeping.  The `setup_server` script should have created the ares user for you automatically and printed the password.  Scroll back if you missed it.
{% endwarning %}

{:start="2"}
2. Copy/paste the following commands into the shell to run them **one by one**.  Wait until one command has completed before pasting the next command.

        curl https://raw.githubusercontent.com/aresmush/aresmush/master/bin/install > install
        
        chmod +x install
        
        ./install
        
        export NVM_DIR="$HOME/.nvm"
        [ -s "$NVM_DIR/nvm.sh" ] && \. "$NVM_DIR/nvm.sh" 

{:start="3"}
3.  Enter the information about your game when prompted.

This will take several minutes.  There will be a lot of spam, but eventually it will say it's done.

## Add a Security Certificate

If you are using a domain name, it is strongly recommended that you configure your web portal with a security certificate, so players can connect securely using HTTPS instead of HTTP. 

1. If you aren't already, log back into the server shell using the **ares** user.
2. Run the following commands:
      
        cd aresmush
        
        bin/certs

3. Follow the prompts.

See [Configuring HTTPS]({{site.baseurl}}/tutorials/install/https.html) for details.

## Reboot the Server

After all of the installation is complete, type `sudo reboot` to reboot the server. This ensures everything comes up working properly.

## Next Steps

Your game should be up and running.  Check out [Next Steps](/tutorials/install/next-steps.html) to learn about connecting to it and testing it out.