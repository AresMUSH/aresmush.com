---
title: Custom Server
description: 
layout: tutorial
installTutorial: true
tutorialName: Installing AresMUSH
tutorialIndex: tutorials/install
prevstep: choosing-a-host
nextstep: getting-a-hostname
tags:
- install
---

Because AresMUSH has different needs than Penn or Tiny, most dedicated "MUSH Hosting" plans won't work.  They won't have enough resources or the right software packages.  Instead, you'll want to get a Virtual Private Server (VPS) or cloud server equivalent that will let you install the software you need.

{% include custom_install_warning.md %}

This article details the system requirements to help you find the right server and get everything set up.

{% include toc.html %}

## Supported Environment

The supported environment for the automated Ares installer is:

* A [DigitalOcean droplet](/tutorials/install/digital-ocean.html).
* 2GB RAM required.  Giant games may need more RAM, but you can always upgrade later.
* Ubuntu Linux (Ares' standard install is 20.04).
* **Nothing but the starter image** installed.   

Hard drive space is not generally a concern. The base install will take only about 1GB of hard drive space, and database sizes are insignificant. Uploaded files (for theme/character images and the like) will be the bulk of your hard drive usage.

## Custom Environments

Of course you are welcome to try your own custom environment.  Maybe you have your own existing server or favored cloud server provider.  Ares has run on OSX and could conceivably run on any linux variant.  

{% tip %}
Support for custom setups is limited.  You're welcome to ask for help but we may not be *able* to help you.  Using a custom environment is only recommended for people with server admin experience (or a server admin buddy).
{% endtip %}

Setting up Ares in a custom environment requires the installation of several software packages: 

* Ruby - runs the game code.  We recommend using Ruby Version Manager (RVM) to control which version of Ruby you get.
* EmberJS - builds the web portal code.
* Redis - the database.
* Ruby's Bundler - installs dependencies for the game code.
* NodeJS and Node Package Manager (NPM) - installs dependencies for the web portal code.
* Git - updates the code to new versions.
* nginx - the web server.  (Ares should work just fine with Apache as well but you're on your own configuring it).

As well as various configuration/setup steps:

* Create the ares user and give it the necessary permissions.
* Copy over the default game configuration files and initialize the database.
* Configure some basic game settings.
* etc.

All of these steps are detailed in the Ares install scripts. Use [`aresmush/bin/setup_server`](https://github.com/AresMUSH/aresmush/blob/master/bin/setup_server) and [`aresmush/bin/install`](https://github.com/AresMUSH/aresmush/blob/master/bin/install) as a **guide** when installing a game on a custom environment.  There are some examples of how to do this below.

{% include custom_install_warning.md %}

### Example 1: Installing the Web Server

Here's an excerpt from the Ares install scripts that deals with the web server (nginx).

    echo -e "${ARES_INSTALL_TEXT} Nginx for web server."
    apt-get install -y nginx

    echo -e "${ARES_INSTALL_TEXT} Install default web configuration."
    sudo cp "${HOME_DIR}/aresmush/install/nginx.default" /etc/nginx/sites-enabled/default

Based on this, you know you need to install the web server and configure it.  However, you may not be able to run these specific commands for a number of reasons:

* Your system might need to use a different package management command (e.g. yum instead of apt-get).  
* You might already have nginx installed with a 'default' config file and don't want to overwrite it.
* You might already have Apache installed and prefer to use that instead.

In those situations, you would need to manually install and/or configure your desired web server using whatever steps are appropriate for your environment.

### Example 2: Using RVM

Here's another excerpt from the Ares install scripts that installs and uses Ruby Version Manager (RVM) to get the right version of Ruby.

    echo -e "${ARES_INSTALL_TEXT} Install RVM."
    \curl -sSL https://get.rvm.io | bash -s stable --ruby
    source "${HOME_DIR}/.rvm/scripts/rvm"
    
    echo -e "${ARES_INSTALL_TEXT} Install Ruby version."
    rvm install ruby-2.6.3

RVM is a convenient way to install Ruby, but RVM might not be compatible with your custom environment.  You might instead use rbenv instead of compile Ruby from source.  

The important thing is that the 'ares' user has access to the right version of ruby and can install gems (libraries) without any goofy permissions errors.

{% note %}
Bear in mind that the above are just examples. You are responsible for adapting the standard Ares install process for your a custom environment.
{% endnote %}