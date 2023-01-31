---
title: DigitalOcean Easy Mode
description: 
layout: tutorial
installTutorial: true
tutorialName: Installing AresMUSH
tutorialIndex: tutorials/install
prevstep: index
nextstep: next-steps
tags:
- install
---

If you're willing to use [DigitalOcean](http://www.digitalocean.com/?refcode=5c07173bc1f2) as your MU host, I'm happy to set up Ares for you. 

{% note %}
There is no installation fee for Easy Mode, but you will still pay DigitalOcean for hosting. Easy mode may take 7-10 days depending on my availability.
{% endnote %}

{% include toc.html %}

## How It Works

Here's how it works in brief (full details follow in the rest of the article):

1. You create a droplet (server) using the Ares 1-click image. You don't have to finish the setup, just create the skeleton.
2. You send me a request with your game information.
3. I will log into your droplet and set it up for you.

> **Full Disclosure:** I get a referral bonus from DigitalOcean if you sign up using [this referral link](http://www.digitalocean.com/?refcode=5c07173bc1f2), but you also get a starter credit. The referral bonus helps keep the doors at [AresCentral](/arescentral.html) open.  Using the referral link is *not* required for Easy Mode, but is appreciated.

## Easy Mode Terms of Service

**THERE IS NO WARRANTY FOR THIS SERVICE, EXPRESS OR IMPLIED.  YOU AGREE THAT THE Author (Wordsmyth Creations) IS NOT RESPONSIBLE FOR ANY DEFECTS IN OPERATION, HARM TO THE GAME OR SERVER, OR ANY OTHER CLAIM, DAMAGES OR LIABILITY RESULTING FROM THE USE OF THIS SERVICE.**

You are responsible for maintaining the server after initial setup, including any software upgrades, security patches, and all associated hosting fees.  

You are also responsible for complying with the game software's [License Agreement](/license.html).

If requesting an AresMUSH.com subdomain, you must also agree to the [AresMUSH Subdomain Terms of Service](/subdomain-tos.html).

## Create the Droplet

Unfortunately, Digital Ocean's tools do not allow me to transfer a completed droplet to you. You'll have to make one, and then I can set it up. To do that:

Create an account on [DigitalOcean](http://www.digitalocean.com/?refcode=5c07173bc1f2) if you don't already have one.  

1. Go to the [AresMUSH 1-click droplet image](https://marketplace.digitalocean.com/apps/aresmush?refcode=5c07173bc1f2) in the DigitalOcean Marketplace.
2. Click "Create Droplet" and use the following options:
  * Select a "Shared CPU" and "Basic" droplet.
  * The 2GB/1CPU droplet will suit most Ares games. Giant games may need more RAM, but you can always upgrade later. Below 2GB is not supported.
  * Don't add block storage.
  * Select a region. New York is a good choice unless your players are predominately from outside the US.
  * Use the **password option** and set a root user password. Save your root password in a safe place. (If you want to use a SSH key, you can set it up after easy mode is complete.)
  * Do **NOT** enable IPv6; Ares does not support dual IP versions, and many PCs can still only access v4.
  {% include pretty_image.html file='/install-ares/install-droplet-2.png' %}

{:start="3"}
3. Once your droplet is created, find the IP address on your DigitalOcean dashboard.

For easy mode, you do not need to complete the rest of the 1-click setup instructions. Just create the droplet and I will do the rest. The [1-click instructions](/install/oneclick.html) are pretty straightforward, though, if you wanted to give it a try yourself.

{% note %}
You are responsible for all server charges for the droplet.
{% endnote %}


## Submit a Request

Once the droplet is created, [email me](/feedback.html) and provide the following information:

1. The IP address AND root password for your droplet.
2. Your desired game port number. (Must be > 1024; default is 4201.)
3. A name and description for your game.  (You can change this later.)
4. Your desired hostname (yourgame.somewhere.com).  You can [request an aresmush.com hostname](/tutorials/install/getting-a-hostname.html) or [register your own](/tutorials/install/getting-a-hostname.html).
5. Whether you want me to install a security certificate for your web portal.  This is highly recommended to ensure security and enable browser notifications.  I will use your email address to register the certificate with https://letsencrypt.org/. 
6. A statement affirming: "I have read and understood the Easy Mode terms of service, AresMUSH license agreement, and (if applicable) the AresMUSH subdomain terms of service."

## Next Steps

After I have ensured everything is running properly, I will contact you with the ares user password. You may then begin using your game. 

{% note %}
It is strongly recommended that you immediately change both the root and ares user passwords as soon as the game is ready to go.
{% endnote %}

Check out [Next Steps](/tutorials/install/next-steps.html) to get started.