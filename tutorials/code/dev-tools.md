---
title: Development Tools
description: 
layout: page
tags:
- code
- tools
---

This article lists some tools that you'll probably want to get if you're doing Ares coding.

{% include toc.html %}

## Code Editors

Do yourself a favor and get a decent code editor for managing code on your local PC. Editors offer syntax highlighting, project browsing/searching, source control integration, and more. Here are some good ones:

* [Visual Studio Code](https://code.visualstudio.com/) - Windows/Mac/Linux
* [Sublime](http://www.sublimetext.com/) - Windows/Mac/Linux
* [Textmate](https://macromates.com/) - Mac Only

## Github Desktop

[GitHub Desktop](https://desktop.github.com/) is a nice tool that makes it easy to work with GitHub.  It's available for Mac or Windows.

For help using GitHub, including GitHub desktop, see the [Git tutorial](/tutorials/code/git.html).

You can use GitHub to move code between your test environment and your real game.

{% include pretty_image.html file='/code/git-test.png' %}

## Test Environment

It's helpful to have a place to test your code that *isn't* your main game.  That way you can make sure everything works right before unleashing it on your players.  

Most games will not need a test environment until after they open to the public. While you're in development, you can generally tolerate a few hiccups on your real server. Once you have a little more experience with Ares or are ready to open, you can explore these other options for setting up a game for development purposes.

### Dual Droplets

The quickest way to set up a test game is to just get a second droplet and install a new copy of the game using the standard [installation instructions](/tutorials/install). Essentially you will have two games running the same code.

You don't need a separate host name for the test game; you can just use the droplet's IP address as the host name.

### Installing Locally

There are a few different options for getting Ares running on your local PC.

{% note %} 
All of these will require some tinkering and technical know-how; expect to get your hands dirty. You can ask for help from the community, of course, but we are not experts in these tools and support is not guaranteed.
{% endnote %}

* **Docker** - Docker's container service lets you run Ares in an Ubuntu Linux environment on your own PC. See [Running Ares With Docker]({{site.baseurl}}/tutorials/code/docker.html) for details.
* **Ansible with Virtual Box** - Virtual Box is a Virtual Machine application that essentially creates your own virtual linux environment, and Ansible automates the installation. Mudpuppy@AresCentral has graciously contributed an installer using [Ansible](https://github.com/Mudpuppy12/ansible-aresmush). This is not officially vetted or maintained by AresMUSH staff.
* **Other VM Software** - Virtual Machine (VM) software will let you run a full instance of Ubuntu Linux on your local PC or Mac. There are [some notes]({{site.baseurl}}/tutorials/code/vm.html) to get you started, but you're on your own for this one.
* **Local Mac Dev** - Ares can run natively on a Mac if you install the individual components. There are [some  notes](https://github.com/AresMUSH/aresmush/blob/master/bin/local_setup_mac) to get you started with Homebrew, but it will require some tinkering.

Ares cannot run natively on a Windows PC due to a limitation of the database libraries.

### Installing on Your Droplet (Not Recommended)

Some games have tried to have a test instance installed on the same droplet as their regular game. You are strongly advised NOT to do this. The droplets aren't built for running two games at once, and it's very easy to accidentally mess up the configuration and/or database on your real game. If you wish to try this, you're on your own.