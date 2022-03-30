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

Do yourself a favor and get a decent code editor.  Here are some good ones:

* [Atom](https://atom.io/) - Windows/Mac/Linux
* [Visual Studio Code](https://code.visualstudio.com/) - Windows/Mac/Linux
* [Sublime](http://www.sublimetext.com/) - Windows/Mac/Linux
* [Textmate](https://macromates.com/) - Mac Only

I personally don't think a Ruby IDE like RubyMine is worth the cost for the benefits you get, but YMMV.

## Github Desktop

[GitHub Desktop](https://desktop.github.com/) is a nice tool that makes it easy to work with GitHub.  It's available for Mac or Windows.

For help using GitHub, including GitHub desktop, see the [Git tutorial](/tutorials/code/git.html).

## Test Environment

It's helpful to have a place to test your code that *isn't* your main game.  That way you can make sure everything works right before unleashing it on your players.  

{% note %} 
It's strongly recommended that you follow the standard [installation instructions](/tutorials/install) for your very first Ares game.  For just a few bucks, less than the price of a grande coffee, you can spin up a droplet for a couple weeks and get your feet wet.  That way you're not trying to learn both Ares code and Ares server setup at the same time!  Once you have a little more experience with Ares, you can explore these other options for setting up a game for development purposes.
{% endnote %}

There are several options available to you.


{% tip %} 
Dual Droplets is the only easy test game setup.  All the rest require some degree of sever administration fiddling.  If that's not your thing, then dual droplets is probably the best solution for you.
{% endtip %}

### Dual Droplets

The simplest and quickest way to set up a test game is to just get a second droplet and install a new copy of the game using the standard [installation instructions](/tutorials/install).

You don't need a separate host name for the test game; you can just use the droplet's IP address as the host name.

### Installing on Your Local Mac

If you have MacOS installed on your home PC, you can actually install your own copy of Ares and run the code locally.

1. Install [Homebrew](https://brew.sh/), Mac's package manager.

2. Copy/paste the following commands into a Mac terminal **one by one**.  Wait until one command has completed before pasting the next command.

        curl https://raw.githubusercontent.com/aresmush/aresmush/master/bin/local_setup_mac > setup_ares
        
        chmod +x setup_ares
        
        ./setup_ares

3. The install script will set up the command-line version of Git, but you probably also want to install [GitHub Desktop](https://desktop.github.com/).  Either one will work for Ares.

4. If you want the Redis database server to be running all the time, set it up as a Homebrew service using `brew services start redis`.  Otherwise you'll have to start it every time you want to use it by typing `redis-server /usr/local/etc/redis.conf`.

5. Clone the aresmush and ares-webportal code repositories to your local drive.  They must reside in adjacent directories (e.g. /home/Users/you/Code/aresmush and /home/Users/you/Code/ares-webportal).  See the [Editing Code](/tutorials/code/edit-code) tutorial for help using GitHub desktop to clone the game.

6. From the aresmush directory, run the following scripts to set up the game:

        cp -r install/game.distr game
        mkdir game/logs
        chmod +x bin/*
        bin/configure
        bin/wipedb

8. Start the game using `bin/devstart` in the aresmush directory.

9. Start the web portal using `bin/devportal` from the ares-webportal directory.  The development web portal runs on http://localhost:4200.

### Installing on Your Local PC

AresMUSH won't run on Windows due to a limitation in the database driver, but you can install Ares using a Virtual Machine (VM).  A VM is like a computer within a computer.  Once your VM is installed and configured, you can connect to it just as you would a server in the cloud.

{% tip %}
Mudpuppy@AresCentral has contributed an automatic installer using [Ansible](https://forum.aresmush.com/t/ansible-installer/509).  This method is not officially supported, but you're still welcome to give it a try and see if it works for you.
{% endtip %}


1. Download and install [Oracle VirtualBox](https://www.virtualbox.org/).
2. Install the VirtualBox Extension Pack (available from the same downloads page as VirtualBox itself).
3. Create a VM in VirtualBox.  Use the following options:
  * type: Linux
  * version: Ubuntu
  * memory: 512MB
  * hard disk: 10GB virtual memory hard disk (VirtualBox Disk Image, fixed size)
4. Download the Ubuntu **Server Install Image**.  The current version is [here](http://releases.ubuntu.com/bionic/ubuntu-18.04.2-live-server-amd64.iso), but this may change over time.  You want the latest 18.04 "server install image".  If you have trouble getting the 64-bit version to work (which apparently can happen on some versions of Windows), you can try the 32-bit "server install image" of 16.04 instead.
5. Start the VM.
6. When asked for the startup disk, browse to and select the Ubuntu ISO image you downloaded.
7. Run through the Ubuntu setup using the default options.  Create an ares user and save its password.
8. The VM will reboot when finished.
9. When the VM restarts, log in.
10. Type `ifconfig`.  This will tell you the VM's **Private IP Address**.
{% include pretty_image.html file='ifconfig.png' %}

{:start="11"}

11. Go to Devices -> Network -> Network Settings -> Adapter1 -> Advanced and select Port Forwarding.
12. Create ports to forward from localhost (127.0.0.1) to the VM's Private IP for ports: 22, 4200, 4201, 4202 and 4203.  This is going to let your local PC connect to the VM.
{% include pretty_image.html file='port-forwarding.png' %}

{:start="13"}

13. Now you should be able to connect to the VM using a SSH client like PuTTY ([Windows](http://www.putty.org/) / [Mac](https://www.ssh.com/ssh/putty/mac/)) by connecting to localhost port 22.  (Say yes to the security key message.)
14. Using SSH, run the `setup_server` script as described in the [install instructions](/tutorials/install/setup-server.html).
15. Then run the `install` script as described in the [install instructions](/tutorials/install/install-game.html).  Use the following options:
  * host: Use the VM's Private IP from above.
  * ports: Use defaults for all ports.
16. Shutdown the VM by doing File -> Power Off.

#### Using the VM

Your VM is now ready to use.  You can leave it powered off whenever you're not using it.  Here are the steps to start the game:

1. Open VirtualBox and start the VM.
2. Open a SSH client shell and start the game in development mode:
    cd aresmush
    bin/devstart
2. Open another SSH client shell and start the web portal in development mode:
    cd ares-webportal
    bin/devportal
3. From your PC, you should now be able to connect to the game using 127.0.0.1 port 4201, and to the web portal using http://localhost:4200.

To change the code on the VM, you can use any of the methods described in the [Editing Code](/tutorials/code/edit-code/) tutorial.  You can edit code directly through the SSH client, upload new code via FTP (the VM will accept SFTP on 127.0.0.1) or use GitHub to push code to the cloud and then pull it down to the server.

### Installing on Your Droplet

You may have heard of some other games that have a test instance installed on the same droplet as their regular server. This is technically possible but not advised because:

* To say it's a PITA to set up is an understatement.
* It is very easy to shoot yourself in the foot and accidentally mess up the configuration and/or database on your real game.
* You will likely cause performance issues on your real game while testing.  The small-sized droplets have enough resources to run one game, not two.
* It's just awkward to use.  The other options are better.

If you choose to go this route, you're on your own.  There are too many pitfalls for me to be comfortable guiding people through the setup.

## Getting Code to the Test Game

You edit code on the test game the same way you do on the real game: through direct editing, FTP, or GitHub.  GitHub offers the most reliable workflow.

1. Develop code on your PC.
2. Push it to GitHub.
3. Pull it to the test game.
4. Load the code on the test game and see how it works.
5. Repeat steps 1-4 as needed, then when you're happy, pull the code to the real game.
6. Reload the code on the real game and go!

{% include pretty_image.html file='/code/git-test.png' %}

For more help using GitHub, including GitHub desktop, see the [Git tutorial](/tutorials/code/git.html).

{% warning %}
Do not use the `upgrade` script or command on test games unless they're running on their own droplet.
{% endwarning %}
