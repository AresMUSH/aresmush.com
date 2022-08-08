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

* [Atom](https://atom.io/) - Windows/Mac/Linux
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

{% note %} 
Most games will not need a test environment until after they open to the public. While you're in development, you can generally tolerate a few hiccups on your real server. Once you have a little more experience with Ares or are ready to open, you can explore these other options for setting up a game for development purposes.
{% endnote %}

### Dual Droplets

The simplest and quickest way to set up a test game is to just get a second droplet and install a new copy of the game using the standard [installation instructions](/tutorials/install). 

{% tip %}
Since your test game will not have many players connected, you can save money using a small droplet size. A general droplet with 1GB of RAM will suffice for most test games. You may even be able to get by on 500MB RAM.
{% endtip %}

You don't need a separate host name for the test game; you can just use the droplet's IP address as the host name.

### Installing on Your Local PC or Mac Using Docker

You can also run Ares on your local PC or Mac using Docker Desktop. Though not technically a "virtual machine", Docker's container service shares many similarities and essentially lets you run Ares in an Ubuntu Linux environment on your own PC.

You will need to get the [Ares Docker](https://github.com/aresmush/ares-docker) files and follow the instructions there.

### Installing on Your Local PC or Mac using a VM

Virtual Machine (VM) software will let you run a full instance of Ubuntu Linux within your local PC or Mac. There are several popular VM software packages out there, including [Oracle VirtualBox](https://www.virtualbox.org/) and [HashiCorp Vagrant](https://www.vagrantup.com/).

{% note %}
Setting up a VM environment requires a fair bit of technical know-how and elbow grease. Docker is generally an easier option. VMs are not officially supported, but you're still welcome to ask for help from the community on either the forum or Discord.
{% endnote %}

You'll want to create a new VM using the Ubuntu base image. From there, you will need to [setup the server](/tutorials/install/setup-server.html) and [install the game](/tutorials/install/install-game.html) just as you would for a regular AresMUSH self-install. Use the VM's **Private IP** for your hostname. You can usually get this from the `ifconfig` command in the server shell.

{% include pretty_image.html file='ifconfig.png' %}

To connect to a game running on the VM, you may need to set up port forwarding. This makes it so when you go to localhost:4200 on your PC the traffic is sent to the VM. For example, you could create ports to forward from localhost (127.0.0.1) to the VM's Private IP (Guest IP) for ports: 22, 4200, 4201, 4202 and 4203. To set this up, you will need to find the Port Forwarding settings on your VM.  Details may vary for your system. Once port forwarding is enabled, you can connect to the game/web portal using localhost:4201 and localhost:4200.

{% include pretty_image.html file='port-forwarding.png' %}

Mudpuppy@AresCentral has graciously contributed an automatic installer using [Ansible](https://github.com/Mudpuppy12/ansible-aresmush) that may help automate the installation onto a VM. This is also not officially supported.

### Installing on Your Droplet (Not Recommended)

You may have heard of games trying to have a test instance installed on the same droplet as their regular server. Getting multiple games running on the same droplet is challenging. It can cause performance issues on your real game, and it's very easy to accidentally mess up the configuration and/or database on your real game. If you choose to go this route, you're on your own.