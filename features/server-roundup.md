---
title: Choosing the Right MU Server
description: 
layout: page
tags:
- features
---

Choosing the right server for your MUSH is important, and Ares is not going to be the best choice for every game.  This article compares some key MUSH features across different servers to help you find the one that best fits your needs.

{% include toc.html %}

## Server List

Here are the servers considered in this article:

* [AresMUSH](http://www.aresmush.com)
* [Evennia](http://www.evennia.com)
* [RhostMUSH](https://github.com/RhostMUSH/trunk)
* [PennMUSH](http://www.pennmush.org)
* [TinyMUX](http://www.tinymux.org/)

Ares, Evennia and Rhost are great modern platforms for making a MU. PennMUSH and TinyMUX are solid choices that have been around forever.

<a name="lego"></a>

## Why *Not* Ares?

MUSH servers are like LEGOs. Many servers come with some basic building blocks and a pile of bricks for you to do your own thing. Ares isn't like that. It's more of a pre-built LEGO castle, all ready to move in and play. You can customize the interior quite a bit, maybe even add on a new tower or two, but you can't easily change the walls and foundation. 

For many games that's perfect. It lets them get up and running quickly with no coding needed.

But if your game vision requires you to start ripping out the castle's walls, it's probably easier to start with a pile of bricks instead.

Some reasons why you might want to think twice about using Ares for your game:

* You prefer everyone to RP on the grid in open scenes. (Ares offers more flexible RP using scenes and temp rooms. Private and asynchronous RP are not stigmatized.)
* You like immersive IC code: elevators, gossip bots, pose-scrambling language code, radios, etc. (These systems really don't mesh with Ares' scene system and web portal.)
* You prefer OOC obfuscation of information - hidden plots, hidden rooms, etc. and minimal OOC interaction. (Ares is designed to be more transparent and community-driven.)
* You hate game wikis.  (Ares' web portal is an integral part of the game.)
* You can't live without multi-word character names. (Ares just doesn't support this, though there's a nickname system that might be an acceptable substitute.)

## Basic Systems

This chart shows what basic game commands/systems each server offers.  

Obviously this is biased a bit from my perspective, but I have done my best to be fair and accurate in representing the other servers.  If you see any discrepancies, please [let me know](/feedback.html).

> <i class="fa fa-check-square"></i> - The server comes with that functionality out of the box.
> 
> <i class="fa fa-user"></i> - A community contribution is available.  Community contributions usually require coding knowledge to install/configure, and may have limited support.  This list only includes well-known code packages like SGP, Myrddin's BBS, Anomaly Jobs, Faraday/Volund code suites, and approved Evennia/Ares contribs.


|Feature |AresMUSH |Evennia |PennMUSH |TinyMUX |RhostMUSH |
|----|
|Creating / Connecting |<i class="fa fa-check-square"></i> |<i class="fa fa-check-square"></i> |<i class="fa fa-check-square"></i> |<i class="fa fa-check-square"></i> |<i class="fa fa-check-square"></i> |
|Building / Moving |<i class="fa fa-check-square"></i> |<i class="fa fa-check-square"></i> |<i class="fa fa-check-square"></i> |<i class="fa fa-check-square"></i> |<i class="fa fa-check-square"></i> |
|Posing |<i class="fa fa-check-square"></i> | <i class="fa fa-check-square"></i> |<i class="fa fa-check-square"></i> |<i class="fa fa-check-square"></i> |<i class="fa fa-check-square"></i> |
|Channels / Pages |<i class="fa fa-check-square"></i> | <i class="fa fa-check-square"></i> |<i class="fa fa-check-square"></i> |<i class="fa fa-check-square"></i> |<i class="fa fa-check-square"></i> |
|Mail |<i class="fa fa-check-square"></i> |<i class="fa fa-user"></i>|<i class="fa fa-check-square"></i> |<i class="fa fa-check-square"></i> |<i class="fa fa-check-square"></i> |
|BBS / Forums |<i class="fa fa-check-square"></i> |<i class="fa fa-user"></i>|<i class="fa fa-user"></i>|<i class="fa fa-user"></i>|<i class="fa fa-check-square"></i>|
|Advanced Who / Where |<i class="fa fa-check-square"></i> ||<i class="fa fa-user"></i>|<i class="fa fa-user"></i>|<i class="fa fa-user"></i>|
|Events Calendar|<i class="fa fa-check-square"></i> ||<i class="fa fa-user"></i>|<i class="fa fa-user"></i>||
|Admin Jobs |<i class="fa fa-check-square"></i> ||<i class="fa fa-user"></i>|<i class="fa fa-user"></i>|<i class="fa fa-user"></i>|
|Finger / Profile |<i class="fa fa-check-square"></i> ||<i class="fa fa-user"></i>|<i class="fa fa-user"></i>|<i class="fa fa-user"></i>|
|IC Time |<i class="fa fa-check-square"></i> |<i class="fa fa-check-square"></i>|<i class="fa fa-user"></i>|<i class="fa fa-user"></i>|<i class="fa fa-user"></i>|
|Places |<i class="fa fa-check-square"></i> ||<i class="fa fa-user"></i>|<i class="fa fa-user"></i>|<i class="fa fa-user"></i>|
|Weather|<i class="fa fa-user"></i> ||<i class="fa fa-user"></i>|<i class="fa fa-user"></i>||
|Scenes and Repose |<i class="fa fa-check-square"></i> ||<i class="fa fa-user"></i>|<i class="fa fa-user"></i>|<i class="fa fa-user"></i>|

Note that a built-in system is only useful if you like how it works.  If you plan on ripping it all out and writing it from scratch anyway, then it may be easier to start with a blank slate.

## Web Integration

The newer servers have integrated game websites that pull data directly from the game.  Some also support a web-based MU client so you can play from the web.

|Feature|AresMUSH |Evennia |PennMUSH |TinyMUX |RhostMUSH |
|----|
|Integrated Website|Integral Web Portal |Minimal Website (Extensible) |--- |--- |API Only |
|Web Client|Yes|Yes|API Only|---|API Only|

Ares contains a full-fledged [web portal](https://aresmush.com/web-portal/) with an integrated wiki, web chargen, scenes and character profiles, and an admin console. The web portal is an essential part of the game; you cannot remove it.

Evennia comes with an integrated website.  Out of the box it has an admin panel for editing the database and a few player utilities.  You can use the Django web framework to code up a more robust site like [Arx’s](http://play.arxmush.org/).

Rhost supports a web API, which you could use to build an integrated website.  

PennMUSH and Rhost have server-side support for [Grapenut's WebClient](https://github.com/grapenut/websockclient) or a custom-made websocket client, but you have to set up the website yourself.

## Language

The programming language used by the game is relevant if you want to modify or extend the existing code.

|AresMUSH |Evennia |PennMUSH |TinyMUX |RhostMUSH |
|----|
|Ruby / EmberJS |Python / Django |MUSHCode / C|MUSHCode / C++|MUSHCode / C|

Rhost commands can also call out to external scripts written in any language.

C/C++ for Penn/Tiny/Rhost is only used in the hardcode, which most people don't have to modify.

## Coding from a MU Client

|AresMUSH |Evennia |PennMUSH |TinyMUX |RhostMUSH |
|----|
|Limited |Limited |Full |Full |Full |

PennMUSH, TinyMUX and RhostMUSH let you code from your MU client, executing MUSHCode or storing commands on objects.  With a robust permissions and quota systems, you can even allow regular players to create their own code.

Ares and Evennia both offer commands to execute arbitrary python/ruby code, but these are limited to admin-level coders for security reasons.  The bulk of coding in these platforms is done in text files that live on the server.  Even though the code lives on the server, it can be reloaded while the game is running.

## Immersive Code

|AresMUSH |Evennia |PennMUSH |TinyMUX |RhostMUSH |
|----|
|Limited |Yes |Yes |Yes |Yes |

Because Ares offers integral support for both temproom (off-grid) and asynchronous RP, it is not well suited to much of the immersive code you might find on some games. It is also geared around OOC transparency, so there are limited ways to hide things from players. The following sorts of systems are not well-suited to Ares:

* Bartenders or menus in restaurant rooms.
* Private mutters or pose-scrambling language code.
* Travel and space systems.
* Hidden/Restricted/Limited RP areas.
* Secret societies/faction members.

Doing anything resembling this is going to involve [knocking down some walls](#lego) and making massive changes to the core code. If these sorts of features are essential to your game, please give careful thought as to whether Ares is really the best choice. You can also consult with [the community]({{site.baseurl}}/feedback.html) to get more advice about potential pitfalls for your specific ideas.

## Skill Systems

Several servers have community contributions for skill systems.  This list only includes well-known, reputable systems and not every bit of random code floating around the 'net.

|System |Servers |Notes |
|---- |
|[FS3, 3rd Edition](/fs3/fs3-3) |AresMUSH ||
|[FS3, 2nd Edition](http://lynnfaraday.github.io/MUSH/) |PennMUSH |No longer in active development. |
|Cortex |AresMUSH |An old, unsupported version also exists for Penn/Tiny. |
|Fate |AresMUSH | |
|FFG Genesys / Star Wars |AresMUSH | |
|Dahan's Star Wars Sagas |PennMUSH, RhostMUSH |Probably also works on TinyMUX. |
|[Dahan's Star Wars / WEG D6 System](http://www.mushcode.com/File/Dahans-D6-Skills) |PennMUSH |Probably also works on TinyMUX and RhostMUSH.|
|[Thenomain's Chronicles of Darkness (WoD)](https://github.com/thenomain/GMCCG/) |TinyMUX |Probably also works on PennMUSH and RhostMUSH. |

