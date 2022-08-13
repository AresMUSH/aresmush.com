---
title: Connecting to the Server Shell
description: 
layout: page
tags:
- hosting
- manage
- ssh
---

To manage certain parts of your game, you will need to connect to the **Server Shell**, which is like a command prompt for your game server.  This is different than connecting with your MUSH client, because your'e connecting to the **server**, not the game.

## The Ares User

Your server comes with a **root** user. This is basically like the One/Headwiz/God user that has ultimate permissions on your server. You will use root when installing the game, but then tuck it away for safekeeping.

The game installation will create an **ares** user and password.  This is the one you should use from now on.

{% warning %} 
Don't use the 'root' user for any Ares-related tasks once the game is installed. You can mess up your game.
{% endwarning %}

## How to Connect

There are a variety of ways to connect to the server shell depending on your OS and what tools you want to use.

### Using Windows Powershell

On Windows 10 and up, you can connect using Windows Powershell:

1. Open a Powershell window.  (You can use the Windows search to find the Powershell application.)
2. Type `ssh USERNAME@yourgame.somewhere.com`.

### Using Mac Terminal

On MacOSX, you can connect using the Terminal app:

1. Open a Terminal window.  (It's usually under "Utilities" in the Applications menu.)
2. Type `ssh USERNAME@yourgame.somewhere.com`.

### Using a Desktop Client

There are many SSH clients available.  A popular one is PuTTY, available for  [Windows](http://www.putty.org/) [Mac](https://www.ssh.com/ssh/putty/mac/).  Once installed, you can add your game to PuTTY's address book.

{% note %} 
When using a desktop client, it may ask you for a port number.  You'll want to use the default SSH port number (usually 22), and **not** your MUSH's game port number.
{% endnote %}

### Connecting through DigitalOcean

If you used the [DigitalOcean](/tutorials/install/digital-ocean.html) setup instructions, you can connect directly to your droplet using the DigitalOcean control panel.  The console is rudimentary and annoying, but it's a safe fallback if nothing else works for you.  Log into your DigitalOcean account and go to "Access->Launch Console."

## Directories

Once your game is installed, you can use the linux change directory command - `cd` - to change to the folder where the Ares code lives.

    cd - Goes to your home folder.
    cd aresmush - From your home folder, changes to the game folder.
    cd ares-webportal - From your home folder, changes to the web folder.
    
The `ls` command will show you a list of files for your current directory.

### sudo

As mentioned before, never use the 'root' user for any Ares-related operation. Sometimes you may need to do things that require administrator permissions, like rebooting the game. If so, you can use the `sudo` command to execute a command with root/admin permissions.

For example: `sudo reboot` will reboot the server.