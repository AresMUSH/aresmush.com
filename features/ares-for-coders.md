---
title: Ares for Coders
description: 
layout: page
tags:
- features
---

Coding is hard in any language, especially if you've never done it before.  However, Ares code offers some advantages over traditional MUSH softcode.

## Mainstream Languages

All Ares code uses mainstream languages: Ruby and Ember Javascript.  Both are easier to read and understand than traditional MUSH softcode. There are a lot more Ruby/Javascript programmers than softcode programmers, as well as an extensive community for support.

## Tutorials

Ares offers a robust suite of [tutorials](/tutorials/code) to help you learn Ares code from the ground up. We also have a [Discord](/discord.html) for code and game questions where you can get help.

## Plugins

Ares supports a robust **Plugin** system, with its features separated into plugin modules.  Plugins provide all of the player commands - even core functionality like movement, help, descriptions, pages and channels.  They handle game events, responding to things like "character connected" or "game started".

Plugins are highly-configurable, allowing game owners to easily change their functionality just by editing the game configuration.  You can also add **new** commands and web screens with your own plugins, often without touching core code.

You *can* change the core plugins--customizing them or even ripping them out completely and replacing them. For example, a fantasy MUSH might replace the outfits system with one that ties in with a crafting system. However, this is not for faint of heart. Some systems just do not mesh well with Ares' open, transparent RP architecture. Even for systems that are feasible, changing core code can impose significant design and maintenance challenges on the code staff. In many cases a [different MU server]({{site.baseurl}}/features/server-roundup.html) might be a better foundation than Ares.