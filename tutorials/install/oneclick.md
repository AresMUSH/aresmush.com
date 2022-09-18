---
title: DigitalOcean 1-Click Image
description: 
layout: tutorial
installTutorial: true
tutorialName: Installing AresMUSH
tutorialIndex: tutorials/install
prevstep: index
nextstep: next-steps
tags:
- install
- DigitalOcean
---

The AresMUSH 1-Click Droplet lets you quickly set up your own Ares game through [DigitalOcean](http://www.digitalocean.com/?refcode=5c07173bc1f2). It gives you a server (aka droplet) with all the prerequisites already installed. All you need to do is provide your game information.

{% include toc.html %}

## How It Works

Here's how it works in brief (full details follow in the rest of the article):

1. You create a DigitalOcean droplet from the 1-click image, which comes with all the software you need already pre-installed.
2. You configure your game.

> **Full Disclosure:** I get a referral bonus from DigitalOcean if you sign up for an account using [this referral link](http://www.digitalocean.com/?refcode=5c07173bc1f2), but you also get a starter credit. The referral bonus helps keep the doors at [AresCentral](/arescentral.html) open.  Using the referral link is *not* required for the 1-Click Droplet, but is appreciated.

## 1-Click Droplet Terms of Service

**THERE IS NO WARRANTY FOR THIS SERVICE, EXPRESS OR IMPLIED.  YOU AGREE THAT THE Author (Wordsmyth Creations) IS NOT RESPONSIBLE FOR ANY DEFECTS IN OPERATION, HARM TO THE GAME OR SERVER, OR ANY OTHER CLAIM, DAMAGES OR LIABILITY RESULTING FROM THE USE OF THIS SERVICE.**

You are responsible for maintaining the server after initial setup, including any software upgrades, security patches, and all associated hosting fees.  

You are also responsible for complying with the game software's [License Agreement](/license.html).

If requesting an AresMUSH.com subdomain, you must also agree to the [AresMUSH Subdomain Terms of Service](/subdomain-tos.html).

DigitalOcean does not support or endorse the Ares 1-Click Droplet.

## Create a 1-Click Droplet

To get started:

2. Get the [AresMUSH 1-click droplet image](https://marketplace.digitalocean.com/apps/aresmush?refcode=5c07173bc1f2) from the DigitalOcean Marketplace.
3. Click "Create Droplet" and use the following options:
  * Select a "Shared CPU" and "Basic" droplet.
  * The 2GB/1CPU droplet will suit most Ares games. Giant games may need more RAM, but you can always upgrade later. Below 2GB you may have performance issues and trouble upgrading.
  * Don't add block storage.
  * Select a region. New York is a good choice unless your players are predominately from outside the US.
  * Select an SSH key for logging in (if you don't know what that is, just select the password option) and any other options desired.
  * Do **NOT** enable IPv6; Ares does not support dual IP versions, and many PCs can still only access v4.
  {% include pretty_image.html file='/install-ares/install-droplet-2.png' %}

{:start="4"}
4. Once your droplet is created, find the IP address on your DigitalOcean dashboard.

## Getting a Host Name

You can host a game using the raw IP address, but most games will want a domain name. See [Getting a Hostname]({{site.baseurl}}/tutorials/install/getting-a-hostname.html) if if you want to request a `yourgame.aresmush.com` subdomain or set up a custom domain.

{% note %}
If using a domain name, make sure it's set up before continuing with the installation. The game won't be able to run until the hostname is recognized.
{% endnote %}

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

## Set up Your Game

Next you will configure your game settings.

1. Connect to your game using the server shell using the **root** user, as described above.
2. Make sure your domain registration has gone through by typing `nslookup YOURDOMAINNAME`. You should see your IP address returned.
3. Run the following commands: 

        cd /etc/aresmush
        
        ./complete_setup.sh

5. Enter the information about your game when prompted.

The installation will take several minutes.  There will be a lot of spam, but eventually it will say it's done.

## Add a Security Certificate

If you are using a domain name, it is strongly recommended that you configure your web portal with a security certificate, so players can connect securely using HTTPS instead of HTTP. 

1. Log in to your server shell, but this time use the **ares** user.
2. Run the following commands:
      
        cd aresmush
        
        bin/certs

3. Follow the prompts.

See [Configuring HTTPS]({{site.baseurl}}/tutorials/install/https.html) for details.

## Reboot the Server

After all of the installation is complete, type `sudo reboot` to reboot the server. This ensures everything comes up working properly.

## Next Steps

Your game should be up and running.  Check out [Next Steps](/tutorials/install/next-steps.html) to learn about connecting to it and testing it out.
