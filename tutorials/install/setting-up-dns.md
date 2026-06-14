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

1. [Create a droplet](/tutorials/install) -- **don't** complete the install, just do the first step when you create the droplet and get an IP address. You can find the IP on your Digital Ocean dashboard.
{% include pretty_image.html file='/install-ares/droplet-ip.png' %}

{:start="2"}
2. Create a Namecheap account and purchase the domain.
3. In your Namecheap account dashboard, click "Manage" next to your domain name.
4. Click "Advanced DNS".
5. Click "Add New Record".  (You might need to scroll down a little bit to see the button.)
{% include pretty_image.html file='/install-ares/namecheap.png' %}

{:start="6"}
6. A little editor will appear where you can enter the new domain mapping.
  * Select "A Record".
  * Enter "@" for the "Host".
  * Enter your droplet's IP address for "IP Address".
  * Leave the TTL setting as "Automatic".
  * Click the green checkmark to save.
7. **Wait** for the DNS to update. See below.
8. Once the DNS is recognized by the droplet, complete your game installation.

<a name="propagation" class="anchor"></a>

## DNS Updates

Whenever you create or update your DNS information, it takes time for that to propagate through the internet.

{% tip %} 
DNS updates can take up to 24 hours to be recognized, but usually it only takes 1 hour. 
{% endtip %}

You can tell that the hostname is working by logging into the server shell and typing: `nslookup YOURDOMAINNAME`. 

{% note %}
Be sure to run this command <b>on the droplet</b>. It doesn't matter if your PC can see the DNS update; the installation will only work if the droplet sees it.
{% endnote %}

When the "non-authoritative answer" part of the response lists your droplet's IP address, that means the DNS is working and you can continue with the game installation. If you get a 'not found' answer, the droplet hasn't seen the DNS update yet.

```
ares@mydroplet:~$ nslookup yourgame.com
Server:		127.0.0.53
Address:	127.0.0.53#53

Non-authoritative answer:
Name:	yourgame.com
Address: YOUR_IP_IS_HERE
```

