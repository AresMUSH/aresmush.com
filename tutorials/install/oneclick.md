---
title: DigitalOcean One-Click Image
description: 
layout: page
tags:
- install
- DigitalOcean
---

** IN DEVELOPMENT; DO NOT USE**

Get the image
Create droplet
Set up domain
Use nslookup to ensure domain is recognized

ssh root@YOURGAME

cd /etc/aresmush
./complete_setup.sh


Log in with ares user (ssh key or password)

cd aresmush
bin/certs   (follow prompts - ask for email)  see [Configuring HTTPS](/tutorials/install/https.html))
sudo reboot

