---
title: Getting a Host Name
description: 
layout: tutorial
installTutorial: true
tutorialName: Installing AresMUSH
tutorialIndex: tutorials/install
prevstep: choosing-a-host
nextstep: ports
tags:
- install
- hosting
---

Host names are optional - you can always connect to a game using its IP address.  But it's nice to have a host name (like yourmush.somemuhost.com) so people can remember your game address more easily.

{% note %}
If using a host name, make sure it's set up before continuing with the installation. The game won't be able to run until the host name is recognized.
{% endnote %}

## AresMUSH Domain

You can request an AresMUSH sub-domain (yourmush.aresmush.com). See [Subdomain Terms of Service](/subdomain-tos.html) for details.

## Custom Domain

You can also register a custom domain name (yourmush.com) for just a few dollars a year. There are many domain provider available. I like [Namecheap](https://www.namecheap.com/){:target="blank"} personally, but any will work. [Forbes](https://www.forbes.com/advisor/business/software/best-domain-registrar/){:target="blank"} has a list comparing some of the big ones.

Once you have a domain, you will need to create an "A Record" DNS entry and point it at the IP address of your droplet.  The steps will vary depending on the domain provider. See [Setting Up Domain Hosting With Namecheap](/tutorials/install/setting-up-dns.html) for an example.