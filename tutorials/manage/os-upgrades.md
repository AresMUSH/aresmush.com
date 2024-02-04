---
title: Server OS Upgrades
description: 
layout: page
tags:
- manage
- code
- upgrade
---

The Ares installer will enable automatic installation of critical OS patches, including security updates. These are generally minor and targeted. You will be asked to restart your server occasionally as a result of these upgrades, but otherwise they will be transparent to you.

For most games, these updates alone should be sufficient to keep your game running smoothly.

Sometimes you may see notices about there being a newer version of the Operating System (Ubuntu) available.  Should you upgrade?

**In general, no.**

Linux/ubuntu server upgrades are nowhere near as seamless as Windows or App updates, and most MU owners are not professional server admins used to dealing with the kinds of issues that result. Ruby in particular gets cranky and needs to recompile stuff when you change the OS. Redis also can have config collisions when it gets upgraded. 

If you do decide to upgrade your OS to the next major version, be aware that **it will probably take some technical fiddling to get your game working after a major upgrade.** Proceed at your own risk.

## Issues After Upgrading

If you do decide to upgrade your server OS and run into trouble (like the game not starting or weird Ruby errors) here are a few things to try:

* Use `rvm reinstall <ruby version>` to reinstall ruby. You may also need to do `rvm reload`. Worst case, you can remove and reinstall RVM entirely.
* There may be new libraries you need to install, particularly `ruby-dev`.
* Clear out your `tmp` and `node_modules` directories in the web portal.
* Check your redis config file and ensure that the password matches the one the game’s using.
* Sometimes Apache gets turned on automatically, which will prevent the Ares web server from starting. Disable Apache using `sudo systemctl disable apache2`.

If you have questions, feel free to reach out and I’ll try my best to help. But since this is all at the OS level and not really Ares-specific, my ability to help may be limited.