---
title: Changing the Domain Name
description: 
layout: page
---

When your game is first set up, you choose a domain name, like `yourgame.aresmush.com`.  It's kind of a pain to change this after the game is installed, but it can be done.  

These instructions assume some technical know-how to edit files on the server shell.  Don't hesitate to [ask for help](/feedback.html) if you run into trouble.

{% note %}
Even if you try to keep the old domain name, it will only work on the web side. The game side (with a MU client) cannot listen on multiple domain names at once.
{% endnote %}

1. Update your NEW domain host to point the new domain name to the game server.
2. Ensure that the new domain is visible to the server.  From the server shell, type `nslookup yourgame.somewhere.com`.
    * If the domain is visible, it will show a "non-authoritative answer" with your IP address.
    * It may take up to 24 hours after changing domain information before the server can see the new domain.
3. **DO NOT PROCEED** until the new domain is visible to the server.
4. In the web portal, go to Admin->Setup and edit server.yml.  Set `hostname` to the new domain.
5. [Shut down](/tutorials/manage/shutdown.html) the game engine.
6. Edit the nginx configuration file and replace all instances of your old host with the new host name.  
    * You can edit this using `sudo nano /etc/nginx/sites-enabled/default`.
    * If you want to KEEP the old domain too, your `server_name` will EITHER need to use the catchall (`_`) OR a list of domains: `server_name YOUR_OLD_DOMAIN YOUR_NEW_DOMAIN;`
7. Restart the nginx web server using `sudo service nginx restart`.
8. If you had a security certificate installed, you will need to update certbot.
    * To DELETE the old domain and just start from scratch with the new one:
        * Remove the "managed by cerbot" lines from the nginx config.
        * Restart the nginx web server using `sudo service nginx restart`.
        * Run `sudo certbot delete`.
        * Redo the [HTTPS security certificate installation](https://aresmush.com/tutorials/install/https.html).
    * To KEEP the old one and ADD the new one too:
        * Run `sudo certbot --expand --nginx -d YOUR_OLD_DOMAIN -d YOUR_NEW_DOMAIN`
9. Reboot the server.  When it comes back up, you should be good to go with your new host name.
