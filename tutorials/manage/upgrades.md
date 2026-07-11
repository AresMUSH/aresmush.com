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

| Scenario | Special Handling |
| ---- | ---- |
| Custom Code Changes | See [Upgrading With Custom Code Changes](#upgrading-with-custom-code-changes) |
| Non-Standard Server | See [Upgrading With a Custom Environment](#upgrading-with-a-custom-environment) |
| Release notes say "restart required" | See [Upgrade With a Restart](#upgrade-with-a-restart) |
| Release notes have an "Upgrade Notes" section. | Follow the special instructions in the notes. |

If none of those apply, upgrades are super easy.

From the web portal (in v0.54 and higher):

1. Go to Admin -> Manage -> Upgrade.
2. Select 'Upgrade'.
3. Check the output for errors.

**-or-** From the game (in your usual MU client):

1. Type `upgrade/start` to do the first part of the upgrade.
2. Check the output for errors.
3. When the first part has finished and all errors resolved, type `upgrade/finish` to complete the upgrade.


{% tip %}
If you get error messages about divergent branches or merge conflicts, you will need to resolve those. See [Resolving GitHub Conflicts](/tutorials/code/git-conflicts.html) or [ask for help](/feedback.html).
{% endtip %}


<a name="restart" class="anchor"></a>

## Upgrade With a Restart

Some upgrades affect the core game engine and require that the game be shut down and restarted.  The release notes or the upgrade process will tell you when a restart is required.

To restart the game:

1. Type `upgrade/start` to do the first part of the upgrade.
2. Check the output for errors. If there are any, you will need to resolve them first. See [Resolving GitHub Conflicts](/tutorials/code/git-conflicts.html) or [ask for help](/feedback.html).
3. When the first part has finished and all errors resolved, use the `shutdown` command in-game or Admin -> Manage -> Shutdown from the web portal to shut down the game. (See [Shutting Down the Game](/tutorials/manage/shutdown.html) for help.)
3. Log into the server shell and run `bin/startares` from the aresmush directory. Alternately, you could reboot the entire server.

<a name="fork" class="anchor"></a>

## Upgrading With Custom Code Changes

When you start touching the core code (outside of community plugins or custom hooks), your upgrade process becomes more involved.

If you have your own GitHub fork, here's how you upgrade:

1. Update your fork to get the latest Ares code into your repository.  This will vary depending on what tool you're using, and you can find many GitHub tutorials online.  The [Using GitHub](/tutorials/code/git.html#video-tutorial) video tutorial gives an example walkthrough using GitHub Desktop.  
2. Make sure any conflicts are resolved. See [Resolving GitHub Conflicts](/tutorials/code/git-conflicts.html).
3. Make sure your game is set up to pull code from your own fork.  See [Using GitHub](/tutorials/code/git.html#making-the-game-use-the-fork) if you 
4. Continue the normal upgrade process, using either the [Basic Upgrade](#basic-upgrades) or [Upgrade with a Restart](#upgrade-with-a-restart) depending on whether the upgrade requires a game restart.

If you are not using GitHub, you really should. When you have custom code, upgrades become nigh-impossible without GitHub, and you're on your own if you attempt it.

<a name="conflict" class="anchor"></a>

### Resolving Conflicts

When you change core code, there's a risk that you change something that ALSO changes in core. This results in something called a "merge conflict". For example - you changed a button from A to B, but core changed it from A to C. You'll have to decide whether you want the button to be B, C, or some hybrid of the two. 

See [Resolving GitHub Conflicts](/tutorials/code/git-conflicts.html) for details.


## Upgrading With a Custom Environment

Custom environments are not officially supported. The upgrade scripts are designed with the standard install environment in mind. If you have a custom environment, you may need to tweak paths (notably the standard install directories of `/home/ares/aresmush` and `/home/ares/ares-webportal`) or other commands. 

## Upgrading Community Contribs

Community contributions (plugins or themes) are upgraded independently from the main code.  See [Upgrading Plugins](/tutorials/code/contribs.html#updating-plugins).


## Upgrading the Server OS

See [Server OS Upgrades](/tutorials/manage/os-upgrades.html).