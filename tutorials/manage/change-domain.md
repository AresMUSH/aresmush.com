---
title: Changing the Domain Name
description: 
layout: page
---

When your game is first set up, you choose a domain name, like `yourgame.aresmush.com`.  It's kind of a pain to change this after the game is installed, but it can be done.  

{% note %}
These instructions assume some technical know-how to edit files on the server shell.  Don't hesitate to [ask for help](/feedback.html) if you run into trouble.
{% endnote %}

1. Update your domain host to point the new domain name to the game server.  If you've got an aresmush.com domain, [contact Faraday](/feedback.html).  
    * If your game already has players, you probably want to leave the old hostname also still pointing to the server. 
2. Ensure that the new domain is visible to the server.  From the server shell, type `nslookup yourgame.somewhere.com`.
    * If the domain is visible, it will show a "non-authoritative answer" with your IP address.
    * It may take up to 24 hours after changing domain information before the server can see the new domain.
3. **DO NOT PROCEED** until the new domain is visible to the server.
4. In the web portal, go to Admin->Setup and edit server.yml.  Set `hostname` to the new domain.
5. [Shut down](/tutorials/manage/shutdown.html) the game engine.
6. Edit the nginx configuration file and replace all instances of your old host with the new host name.  
    * You can edit this using `sudo nano /etc/nginx/sites-enabled/default`.
    * If you've installed the security certificate, also remove the lines that say "managed by certbot".
    * If you have players who might connect to the old address, you can put both addresses under the `server_name`.  For example: `server_name  example.org  www.example.org;`
7. Restart the nginx web server using `sudo service nginx restart`.
8. If you had a security certificate installed:
    * Use `sudo certbot delete` to delete the current HTTPS certificate.
    * Redo the [HTTPS security certificate installation](/tutorials/install/https.html).
9. Reboot the server.  When it comes back up, you should be good to go with your new host name.

