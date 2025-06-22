---
title: Finding Code
description: 
layout: tutorial
editCodeTutorial: true
tutorialName: Editing Code
tutorialIndex: tutorials/code/edit-code
nextstep: direct-edit
tags:
- code
---

Before you can actually edit the code, you need to figure out **which** code you want to edit.  To do that, it's helpful to understand a little about how the Ares code is organized.

## AresMUSH Directory

The main AresMUSH game code is organized in a single directory, typically named `aresmush`.  Within that directory are several folders.  Here are the ones you'll most commonly be working with:

* bin - Scripts that you can execute.  For example, `bin/startares` starts the game.
* game - Files specific to your game, like configuration and styles.  Website file uploads live here too.
* plugins - Contains folders for each plugin.

There are some other folders, like engine (for the engine code) and install (for installation utilities), but you shouldn't need to mess with these.  If you find yourself needing to change the engine code, consider [asking first](/feedback.html) because there may be a different way to approach your problem.

### Plugin Organization

The plugin folders all follow a standard structure.  The folders should be pretty self-explanatory (commands is where the command files live, help is where the help files live, etc.) with a few exceptions:


| File/Folder | Purpose |
| ---- | 
| yourpluginname.rb | This file tells the game engine basic information about the plugin. Every plugin has one, and the name always matches the plugin folder. |
| helpers.rb | Often you'll find that many commands in a plugin require similar error checks and/or actions. Helpers let you put that code in one place so that it can be shared throughout the plugin. This lets you avoid duplication, so if you need to change it later you only have to change one place.  For example:  `aresmush/plugins/describe/helpers.rb` contains a common error check to see whether the enactor has permissions to describe the thing:  `Describe.can_describe?(enactor, model)`. A few plugins have multiple helper files named by category. |
| public/* | APIs let plugins talk to each other - getting information or taking actions. They also define the database models and fields available. For example: `Mail.send_mail` is an API in the mail plugin that allows any plugin to send mail. They are basically cross-plugin helpers. |

For more details on plugin directories, see [Plugins](/tutorials/code/plugins.html) when you're ready.


## Ares-Webportal Directory

The web portal code is organized in a separate directory, typically named `ares-webportal`.  The web portal is not as plug-and-play as the main game server, just due to the nature of web development.  You probably want to hold off on trying to edit web portal code until you're a pretty experienced Ares coder.

## Searching Code

You can easily find a specific variable/function/etc. if your code editor supports a folder search.  Many of the editors listed in [Development Tools](/tutorials/code/dev-tools.html) will do that.  If you don't have a folder search, you can also search a repository's code in GitHub.