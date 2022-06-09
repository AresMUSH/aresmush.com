---
title: Configuring HTTPS
description: 
layout: tutorial
installTutorial: true
tutorialName: Installing AresMUSH
tutorialIndex: tutorials/install
prevstep: install-game
nextstep: next-steps
tags:
- install
- config
- https
---

It is strongly recommended that you configure your web portal with a security certificate, so players can connect securely using HTTPS instead of HTTP.  Some browsers will issue security warnings if a website is not on HTTPS, which can turn away players. [CertBot](https://certbot.eff.org/) comes pre-installed in the default Ares installation; you just need to set it up for your domain.

{% tip %}
Using HTTPS requires a domain name. You can't do it if your game is running solely on an IP address.
{% endtip %}

1. From the aresmush directory, run `bin/certs`.
2. Follow the prompts. You will need to:
  * Enter your hostname (e.g., yourgame.aresmush.com).
  * Provide an email to certbot for registration purposes.
  * Agree to the Certbot terms of service.

3. Reboot the server.  See [Rebooting the Server](/tutorials/manage/reboot.html).

4. It may take a few minutes for the server to reboot.  When it does, test out the web portal (you probably need a force-refresh in your browser) and the game.

{% note %} 
These instructions only apply to the default Ares installation. If you are doing a custom install, you'll need to follow the instructions on the [CertBot](https://certbot.eff.org/) website to install Certbot first.
{% endnote %}

#### Certificate Renewal

Security certificates expire after 90 days.  If all went well with your install, CertBot should automatically renew your certificates when they expire.  If you get a security warning saying that your certificate is invalid when viewing the web portal, you may need to [reboot the server](/tutorials/manage/reboot.html) so that the game and web portal recognize the renewed certificate.

#### Devstart and HTTPS

The `bin/devstart` command to run the game in dev mode will not work if HTTPS is enabled.  Instead you must run the start command manually: `bundle exec rake startares`

#### MUSH Client SSL

This feature only applies to the web portal.  Ares does not currently support a SSL connection through standard MU clients.

