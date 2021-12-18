---
title: Upgrades
description: 
layout: page
tags:
- manage
- code
- upgrade
---

At some point there will be a new version of Ares code available and you'll want to upgrade the code on the game server.

{% note %} 
Ares has a lot of support for **upgrades** but not for *downgrades*.  In the unlikely event you need to revert back to a previous version, it's best to [ask for help](/feedback.html) before attempting it. 
{% endnote %}


{% include toc.html %}


## Basic Upgrades

There are a few special conditions that require advanced upgrade procedures.

* If you've made custom code changes, see [Upgrading With Custom Code Changes](#upgrading-with-custom-code-changes) below.
* If you didn't use the standard install scripts and have a custom environment, see [Upgrading With a Custom Environment](#upgrading-with-a-custom-environment) below.
* If the release notes say that a game restart is required, see [Upgrade With a Restart](#upgrade-with-a-restart) below.
* If the release notes have any **special upgrade notes**, you may need to take additional steps as specified in the release notes.

If none of those apply, upgrades are super easy.

From the web portal (in v0.54 and higher):

1. Go to Admin -> Manage -> Upgrade.
2. Select 'Upgrade'.

**-or-** From the game (in your usual MU client):

1. Type `upgrade/start` to begin the upgrade.
2. Type `upgrade/finish` to complete the upgrade.

{% tip %}
You may see messages like  "Your branch is ahead by 4 commits."  You can ignore those.  If you see any other weird messages or errors, [ask for help](/feedback.html).
{% endtip %}

## Upgrade With a Restart

Some upgrades affect the core game engine and require that the game be shut down and restarted.  The release notes or the upgrade process will tell you when a restart is required.

To restart the game:

1. Type `upgrade/start` to begin the upgrade.
2. Use the `shutdown` command in-game or Admin -> Manage -> Shutdown from the web portal to shut down the game. (See [Shutting Down the Game](/tutorials/manage/shutdown.html) for help.)
3. Log into the server shell and run `bin/startares` from the aresmush directory. (See [Starting the Game](/tutorials/manage/start.html) for help.)

## Upgrading With Custom Code Changes

When you start making custom code changes, your upgrade process becomes more involved. The specifics depend on how you're managing your code.  Don't be afraid to [ask for help](/feedback.html) if you're not sure what to do.

### Using GitHub

If you have your own GitHub fork, here's how you upgrade:

1. Update your fork to get the latest Ares code into your repository.  This will vary depending on what tool you're using, and you can find many GitHub tutorials online.  The [Using GitHub](/tutorials/code/git.html#video-tutorial) video tutorial gives an example walkthrough using GitHub Desktop.  
2. Make sure any conflicts are resolved, as described in 'Resolving Conflicts' below. 
3. Make sure your game is set up to pull code from your own fork.  See [Using GitHub](/tutorials/code/git.html#making-the-game-use-the-fork) if you 
4. Continue the normal upgrade process, using either the [Basic Upgrade](#basic-upgrades) or [Upgrade with a Restart](#upgrade-with-a-restart) depending on whether the upgrade requires a game restart.

### Not Using GitHub

If you've been making changes via FTP or direct editing, here's how you upgrade:

1. Type `upgrade/start` in-game to commit any local changes and get the latest game code from GitHub. If you see any CONFLICT notices from the upgrade, you'll need to edit the code on the server shell as explained in 'Resolving Conflicts' below.
2. Continue the normal upgrade process, using either the [Basic Upgrade](#basic-upgrades) or [Upgrade with a Restart](#upgrade-with-a-restart) depending on whether the upgrade requires a game restart.

## Upgrading With a Custom Environment

The upgrade scripts are designed with the standard install environment in mind--notably the standard install directories of `/home/ares/aresmush` and `/home/ares/ares-webportal`. If you have a custom environment, you'll need to tweak the path/user names for the scripts in the 'bin' directory of both the game and web-portal. [Ask for help](/feedback.html) if you're not sure what to do.

## Resolving Conflicts

Sometimes there may be conflicts between code that changed in the new version and code/configuration changes you've made yourself.  When that happens, you'll see a message during the upgrade like:

    CONFLICT! Merge conflict in plugins/channels/channels.rb

You'll need to edit the files in question to resolve the conflict.  You'll see lines like this where there are conflicts between your code and the main Ares code:

    Some code.
    <<<<<<< HEAD
    your original version will be in this section
    =======
    the upgraded main Ares code will be in this section
    >>>>>>> master

Edit the file manually to choose which version you want, and get rid of all the `<<< >>>` junk.  The final file should look clean, like:

    Some code.
    your modified code

Sometimes, rather than dealing with the conflict it's easier to just copy/paste the code for that file from [GitHub](http://github.com/aresmush/aresmush) and start fresh.  Once you have the new main Ares version, you can redo your custom changes.

If you run into trouble resolving conflicts, don't be shy about [asking for help](/feedback.html).

## Upgrading Community Contribs

Community contributions (plugins or themes) are upgraded independently from the main code.  See [Upgrading Plugins](/tutorials/code/contribs.html#updating-plugins).


## Upgrading the Server OS

See [Server OS Upgrades](/tutorials/manage/os-upgrades.html).