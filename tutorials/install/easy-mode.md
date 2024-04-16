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
There is no installation fee for Easy Mode, but you will still pay DigitalOcean for hosting. Easy mode requests typically take about a week to process, depending on my availability.
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

## Step 1 - Create the Droplet

Unfortunately, Digital Ocean's tools do not allow me to transfer a completed droplet to you. You'll have to make one, and then I can log in and set it up.

{% note %}
You are responsible for all billing charges for the droplet once it's created.
{% endnote %}

You'll need an account on [DigitalOcean](http://www.digitalocean.com/?refcode=5c07173bc1f2) if you don't already have one. From your account dashboard:

1. Go to the [AresMUSH 1-click droplet image](https://marketplace.digitalocean.com/apps/aresmush?refcode=5c07173bc1f2) in the DigitalOcean Marketplace.
2. Click "Create Droplet" and use the following options:
  * Select a "Shared CPU" and "Basic" droplet.
  * The 2GB/1CPU droplet will suit most Ares games. Giant games may need more RAM, but you can always upgrade later. **Below 2GB is not supported.**
  * Don't add block storage.
  * Select a region. New York is a good choice unless your players are predominately from outside the US.
  * Use the **password option** and set a root user password. Save your root password in a safe place. (Do **NOT** configure a SSH key now; you can add one after the installation is complete if desired.)
  * Do **NOT** enable IPv6; Ares does not support dual IP versions, and many PCs can still only access v4.
  {% include pretty_image.html file='/install-ares/install-droplet-2.png' %}

{:start="3"}
3. Once your droplet is created, find the IP address on your DigitalOcean dashboard.


## Step 2 - Submit a Request

Once the droplet is created, submit an installation request using this form:

<a href="https://form.jotform.com/231744260871052" class="btn btn-primary" target="_blank">Request Easy Mode Install<a>  

{% tip %}
You must also send me the **root password** for the droplet, either a PM on the forum/discord (preferred) or via email ([contact me]({% link feedback.md %})). This is necessary so I can log into the droplet and set everything up. After the install is complete, you can reset the passwords and I will no longer have access. If you are not comfortable sending the root password, consider the [one-click self-install]({% link tutorials/install/oneclick.md %}) instead.
{% endtip %}

## Next Steps

After I have ensured everything is running properly, I will contact you with the ares user password. You may then begin using your game. 

{% note %}
It is strongly recommended that you immediately change both the root and ares user passwords as soon as the game is ready to go. Use the `passwd` command in the server shell to change the ares password. Use your Digital Ocean dashboard to change the root password. 
{% endnote %}

Check out [Next Steps](/tutorials/install/next-steps.html) to get started.