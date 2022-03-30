---
title: Digital Ocean Easy Mode
description: 
layout: tutorial
installTutorial: true
tutorialName: Installing AresMUSH
tutorialIndex: tutorials/install
prevstep: choosing-a-host
nextstep: next-steps
tags:
- install
---

If you're willing to use [Digital Ocean](http://www.digitalocean.com/?refcode=5c07173bc1f2) as your MU host, I'm happy to set up Ares for you.  

{% include toc.html %}

## How It Works

Here's how it works:

1. Submit a request and receive a Digital Ocean snapshot image.
2. Clone your own server from the snapshot.
3. Finalize your hostname settings.

These steps are described in more detail in the next few sections.

> **Full Disclosure:** I get a referral bonus from Digital Ocean if you sign up using [this referral link](http://www.digitalocean.com/?refcode=5c07173bc1f2), but so do you!  You get starter credit (basically a month free), and the referral bonus helps keep the doors at [AresCentral](/arescentral.html) open.  Using the referral is not required for Easy Mode, but it is appreciated.

## Easy Mode Terms of Service

**THERE IS NO WARRANTY FOR THIS SERVICE, EXPRESS OR IMPLIED.  YOU AGREE THAT THE AUTHOR (Faraday) IS NOT RESPONSIBLE FOR ANY DEFECTS IN OPERATION, HARM TO THE GAME OR SERVER, OR ANY OTHER CLAIM, DAMAGES OR LIABILITY RESULTING FROM THE USE OF THIS SERVICE.**

You are responsible for maintaining the server after initial setup, including any software upgrades, security patches, and all associated hosting fees.  

You are also responsible for complying with the game software's [License Agreement](/license.html).

If requesting an AresMUSH.com subdomain, you must also agree to the [AresMUSH Subdomain Terms of Service](/subdomain-tos.html).

## Submit a Request

Create an account on [Digital Ocean](http://www.digitalocean.com/?refcode=5c07173bc1f2) if you don't already have one.  Then [contact me](/feedback.html) and provide the following information:

1. The email address associated with your Digital Ocean account.
2. Your desired game port number. (Must be > 1024; default is 4201.)
3. A name and description for your game.  (You can change this later.)
4. Your desired hostname (yourgame.somewhere.com).  You can request an aresmush.com hostname or [register your own](/tutorials/install/getting-a-hostname.html).
5. If you want me to install a security certificate for your web portal.  This is highly recommended to ensure security and enable browser notifications.  Setting up HTTPS will require me using your email to register the certificate with https://letsencrypt.org/.
6. A statement affirming: "I have read and understood the Easy Mode terms of service, AresMUSH license agreement, and (if applicable) the AresMUSH subdomain terms of service."

{% note %} 
Your email is needed to transfer the server snapshot image to you.  It must match the email you used for your Digital Ocean account.  I pledge not to do anything nefarious with your email.  See our [privacy policy](/privacy.html) for details.
{% endnote %}

## Clone Your Server

I will transfer a Digital Ocean snapshot image to your account. This image has everything you need to clone a droplet (aka server) with Ares installed on Ubuntu Linux.

{% note %} 
You have seven days to accept the transfer otherwise the request will be aborted.  You are responsible for the server costs once you accept the transfer.
{% endnote %}

1. Log into your Digital Ocean account.  
2. Go to 'Images' and you should see a pending snapshot transfer request.  Click 'Accept'.
3. Now on the 'Images' page you should see the snapshot.  Select 'Create Droplet' to turn that snapshot image into a droplet (aka server).
{% include pretty_image.html file="install-ares/create-droplet-2.png" %}
{:start="4"}
4. Set up your droplet options:
  * The 2GB droplet will suit most Ares games. Giant games may need more RAM, but you can always upgrade later. You *can* get by on 1GB if need be, but it will require some extra work during upgrades.
  * Select 1 droplet, and enter a name for it (like 'ares').
  * All other options may be left as the defaults.
  * Please do **NOT** add an SSH key to your droplet at this time, since I will then not be able to log in to complete the installation. You can add one later once the game is set up.
5. You can keep the snapshot around as a backup until you're sure your server is up and running, but then you should delete it.

## Finalize the Hostname Settings

Hostnames are linked to IP addresses, so you can't fully set them up until you have cloned a droplet from the snapshot.  

If you're using an aresmush.com hostname, simply [contact me](/feedback.html) with your droplet's IP address (visible on the 'Droplets' screen in your Digital Ocean account).  

If you're using your own custom host name, you'll need to set up the DNS yourself. The steps will vary depending on the domain provider. See [Setting Up Domain Hosting With Namecheap](/tutorials/install/setting-up-dns.html) for an example.

{% note %} 
The hostname may take up to 24 hours to be recognized.  
{% endnote %}

You can tell that the hostname is working when you're able to see the web portal when you go to `http://yourmushaddress`.  (There will be a Sad Picard error message, but that's OK for now.)  Once this happens, you'll need to [restart the game](/tutorials/manage/shutdown.html) for everything to start working. 

## Next Steps

Your game should be up and running.  Check out [Next Steps](/tutorials/install/next-steps.html) to learn about connecting to it and testing it out.
