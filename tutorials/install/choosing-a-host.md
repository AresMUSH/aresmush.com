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

MUSHes need to be hosted on a cloud server to make the game accessible to the public.

With a built-in web portal/wiki, a database and more advanced coding tools, Ares cannot run on the limited accounts provided by most dedicated "MUSH hosting" services.  You'll need a Virtual Private Server (VPS) where you have admin privileges. I recommend [DigitalOcean](http://www.digitalocean.com/?refcode=5c07173bc1f2).  It's what I use for [AresCentral](/arescentral.html) and what the automated installer is designed for.

## Install Options

There are several ways to get Ares installed.

| Method | Description | Technical Knowledge Required |
| ----- |
| [DigitalOcean 1-Click Droplet](/tutorials/install/oneclick.html) | **\*\*Coming Soon\*\*** Quickly and easily create a DigitalOcean sever with everything you need pre-installed. All you have to do is configure your game information. | Low |
| [DigitalOcean Easy Mode](/tutorials/install/easy-mode.html) | Faraday will set up an Ares game for you on DigitalOcean. May take 7-10 days depending on availability. | Lowest |
| [DigitalOcean Self-Install](/tutorials/install/digital-ocean.html) | DIY instructions for installing a game on your own DigitalOcean server. | Medium |
| [Custom Server Install](/tutorials/install/custom-server.html) | Install Ares in a custom environment using another hosting service. | Medium to High |

## Local Setup

Running on a local computer is not recommended for hosting a real game, but it can be useful for coding and testing.  See [Setting Up a Development Environment](/tutorials/code/dev-tools.html).