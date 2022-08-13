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
There is no installation fee for Easy Mode, but you will still pay DigitalOcean for hosting. Easy mode may take 7-10 days depending on availability.
{% endnote %}

{% include toc.html %}

## How It Works

Here's how it works in brief (full details follow in the rest of the article):

1. You submit a request with your game information.
2. You invite me to your DigitalOcean team temporarily.
3. I will create a droplet with your game fully installed and ready to go.
4. I will transfer the game info to you and leave your DigitalOcean team.

> **Full Disclosure:** I get a referral bonus from DigitalOcean if you sign up using [this referral link](http://www.digitalocean.com/?refcode=5c07173bc1f2), but you also get a starter credit. The referral bonus helps keep the doors at [AresCentral](/arescentral.html) open.  Using the referral link is *not* required for Easy Mode, but is appreciated.

## Easy Mode Terms of Service

**THERE IS NO WARRANTY FOR THIS SERVICE, EXPRESS OR IMPLIED.  YOU AGREE THAT THE Author (Wordsmyth Creations) IS NOT RESPONSIBLE FOR ANY DEFECTS IN OPERATION, HARM TO THE GAME OR SERVER, OR ANY OTHER CLAIM, DAMAGES OR LIABILITY RESULTING FROM THE USE OF THIS SERVICE.**

You are responsible for maintaining the server after initial setup, including any software upgrades, security patches, and all associated hosting fees.  

You are also responsible for complying with the game software's [License Agreement](/license.html).

If requesting an AresMUSH.com subdomain, you must also agree to the [AresMUSH Subdomain Terms of Service](/subdomain-tos.html).

## Submit a Request

Create an account on [DigitalOcean](http://www.digitalocean.com/?refcode=5c07173bc1f2) if you don't already have one.  Then [contact me](/feedback.html) and provide the following information:

1. The email address associated with your DigitalOcean account.
2. Your desired game port number. (Must be > 1024; default is 4201.)
3. A name and description for your game.  (You can change this later.)
4. Your desired hostname (yourgame.somewhere.com).  You can [request an aresmush.com hostname](/tutorials/install/getting-a-hostname.html) or [register your own](/tutorials/install/getting-a-hostname.html).
5. Whether you want me to install a security certificate for your web portal.  This is highly recommended to ensure security and enable browser notifications.  Setting up HTTPS will require me using your email to register the certificate with https://letsencrypt.org/.
6. A statement affirming: "I have read and understood the Easy Mode terms of service, AresMUSH license agreement, and (if applicable) the AresMUSH subdomain terms of service."

{% note %} 
Your email is needed to transfer the server snapshot image to you.  It must match the email you used for your DigitalOcean account. See our [privacy policy](/privacy.html) for details on how your information is protected.
{% endnote %}

## Set Up the Server

I will transfer a customized DigitalOcean snapshot image to your account and create a droplet from that image.

1. Wait for the email indicating that your snapshot is ready.
2. Invite me to your Digital Ocean team, as described in the [DigitalOcean Teams Guide](https://docs.digitalocean.com/products/teams/how-to/create/#invite-team-members){:target="blank"}.
3. Once we are on the same team, I will transfer the snapshot to your account, create the game droplet, and finalize the installation setup.
  * This step includes setting up the domain name if you have requested an aresmush.com subdomain. 
  * If you are using a custom domain, you will need to set up the DNS yourself. The steps will vary depending on the domain provider. See [Setting Up Domain Hosting With Namecheap](/tutorials/install/setting-up-dns.html) for an example.
  * It may take up to 24 hours for the domain name setup to register, and the game will not work until then.
4. Once the game is ready, I will contact you with details on how to connect (including the ares user password). 
5. I will leave your DigitalOcean team, and you take over managing the server.

{% note %}
You are responsible for all server charges once the snapshot image is transferred and game droplet created.
{% endnote %}

## Next Steps

After I have ensured everything is running properly, I will contact you with the ares user password. You may then begin using your game. 

Check out [Next Steps](/tutorials/install/next-steps.html) to get started.