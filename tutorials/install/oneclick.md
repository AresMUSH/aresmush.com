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

1. Go to the [AresMUSH 1-click droplet image](https://marketplace.digitalocean.com/apps/aresmush?refcode=5c07173bc1f2) in the DigitalOcean Marketplace.
2. Click "Create Droplet" and use the following options:
  * Image: AresMUSH image.
  * Droplet Plan:
    * **Basic (Shared CPU)**
    * **Regular Droplet** (you don't need the premium ones)
    * 2GB / 1CPU  (below 2GB is not supported and will not work; you can always upgrade RAM later if you need to. 
  * Don't add volumes block storage.
  * Choose whether to enable automated backups. It's extra peace of mind for a few extra dollars a month. 
    * If you do not choose this option, be sure to back up your game manually.
  * Select an SSH key for logging in if you wish to.
    * If you don't know what that is, switch to the Password tab and enter a root password.
  * Do **NOT** enable IPv6; Ares does not support dual IP versions, and many PCs can still only access v4.
  {% include pretty_image.html file='/install-ares/install-droplet-2.png' %}

{:start="3"}
3. Once your droplet is created, find the IP address on your DigitalOcean dashboard.

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
2. If you're using a domain name, make sure your domain registration has gone through by typing nslookup YOURDOMAINNAME. You should see your IP address returned. You don't need to do this if you're just using an IP address for your game.
3. Run the following commands: 

        cd /etc/aresmush
        
        ./complete_setup.sh

5. Enter the information about your game when prompted.

The installation will take several minutes.  There will be a lot of spam, but eventually it will say it's done.

## Add a Security Certificate

If you are using a domain name, it is strongly recommended that you configure your web portal with a security certificate, so players can connect securely using HTTPS instead of HTTP. 

{% tip %}
You can't use a security certificate without a domain name. If you're just using a raw IP address, skip to the next section.
{% endtip %}

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

## Starting Over

If at any point you need to start over with your oneclick image:

1. Open the Digital Ocean droplet management dashboard.
2. Go to Settings -> Rebuild.
3. Select the AresMUSH image from the image list. (You may need to search for 'aresmush' if it doesn't show up automatically.)
4. Enter the droplet name for security and click "Rebuild".

It will take a few minutes, but then your droplet will be restored to the original oneclick image and you can start the install all over again. This will not affect the droplet's size/region/etc. and shouldn't impact its IP address or domain either.

{% include pretty_image.html file='install-ares/oneclick-rebuild.png' %}
