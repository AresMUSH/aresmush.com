---
title: Getting a Host Name
description: 
layout: tutorial
installTutorial: true
tutorialName: Installing AresMUSH
tutorialIndex: tutorials/install
prevstep: choosing-a-host
nextstep: server-shell
tags:
- install
- hosting
---

Host names are optional - you can always connect to a game using its IP address.  But it's nice to have a host name (like yourmush.somemuhost.com) so people can remember your game address more easily.

Most VPS servers (including DigitalOcean) don't include a host name. If you want a name, you'll have to set one up separately.

{% note %}
Make sure that your hostname is set up before continuing with the installation. The game won't be able to run until the hostname is recognized. (For easy mode, we will work with you directly to take care of this.)
{% endnote %}

## AresMUSH Domain

You can request an AresMUSH sub-domain (yourmush.aresmush.com). See [Subdomain Terms of Service](/subdomain-tos.html) for details.

## Custom Domain

You can also register a custom domain name (yourmush.com) for just a few dollars a year. 

Once you have a domain, you will need to create an "A Record" DNS entry and point it at the IP address of your droplet.  The steps will vary depending on the domain provider. See [Setting Up Domain Hosting With Namecheap](/tutorials/install/setting-up-dns.html) for an example.