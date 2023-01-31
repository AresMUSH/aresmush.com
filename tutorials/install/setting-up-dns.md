---
title: Setting Up A Custom Domain with Namecheap
description: 
layout: tutorial
installTutorial: true
tutorialName: Installing AresMUSH
tutorialIndex: tutorials/install
prevstep: getting-a-hostname
nextstep: ports
tags:
- install
- hosting
- dns
---

If you want a domain name for your game, you have two options:

* Request a free AresMUSH sub-domain (yourmush.aresmush.com), set up for you. See [Subdomain Terms of Service](/subdomain-tos.html) for details.
* Set up your own domain (yourmush.com).

For the second option, consider [Namecheap](https://namecheap.com). They're affordable, and their tools are pretty straightforward. I don't get anything for recommending them; I just like them.

To set up your MUSH's domain on Namecheap:

1. Create an account and purchase the domain.
2. [Create a droplet](/tutorials/install) -- you don't need to complete the install, just do the first step when you create the droplet and get an IP address.
3. Go to your account dashboard.
4. Click "Manage" next to your domain name.
5. Click "Advanced DNS".
6. Click "Add New Record".  (You might need to scroll down a little bit to see the button.)
{% include pretty_image.html file='/install-ares/namecheap.png' %}

{:start="7"}
7. A little editor will appear where you can enter the new domain mapping.
  * Select "A Record".
  * Enter "@" for the "Host".
  * Enter your droplet's IP address for "IP Address".
  * Leave the TTL setting as "Automatic".
  * Click the green checkmark to save.
8. Finish the game installation.

{% note %} 
The hostname may take up to 24 hours to be recognized.  
{% endnote %}

You can tell that the hostname is working by logging into the server shell and typing: `nslookup YOURDOMAINNAME`. When the "non-authoritative answer" lists your droplet's IP address, the DNS is working and you can continue with the game installation.