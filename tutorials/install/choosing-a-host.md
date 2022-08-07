---
title: Choosing a Host
description: 
layout: tutorial
installTutorial: true
tutorialName: Installing AresMUSH
tutorialIndex: tutorials/install
nextstep: digital-ocean
tags:
- install
- hosting
---

A MUSH needs to be hosted on a server.  You have several options available.

## Cloud Hosting

Most MUs are hosted on a cloud server.  This is the best way to make your game accessible to the public.

With a built-in web portal/wiki, a database and more advanced coding tools, Ares cannot run on the limited accounts provided by most dedicated "MUSH hosting" services.  You'll need a Virtual Private Server (VPS) where you have admin privileges.  I recommend [DigitalOcean](http://www.digitalocean.com/?refcode=5c07173bc1f2).  It's what I use for [AresCentral](/arescentral.html) and what the automated installer is designed for.

* If you would like Faraday to set up Ares for you on DigitalOcean, see **[DigitalOcean Easy Mode](/tutorials/install/easy-mode.html)**.
* If you would like to install Ares on DigitalOcean yourself, see **[DigitalOcean Self-Install](/tutorials/install/digital-ocean.html)** for step-by-step instructions.
* If you prefer to find your own host, see **[Custom Server Install](/tutorials/install/custom-server.html)**.

## Local Setup

Running on a local computer is not recommended for hosting a real game, but it can be useful for coding and testing.  See [Setting Up a Development Environment](/tutorials/code/dev-tools.html).