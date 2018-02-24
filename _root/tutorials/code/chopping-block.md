---
title: Chopping Block
description:
layout: page
tags: 
- code
- features
---

While Ares attempts to recreate the PennMUSH/TinyMUX experience on the whole, a few features were deliberately left out for philosophical reasons.  If you find just can't live without them, please provide [Feedback](/feedback).  If enough people are desperate for the feature, it may be considered for a future version.

## Exit Aliases

Some MUSHes go wild with exit aliases.  An exit named "Front Door" would be accessible via "F", "FR", "DOOR", "FRONT", and who knows what else.

Ares only allows you to have a single exit name, which is shown in room descs next to the destination room name.  For example: 

    [R] Restaurant
    [O] Town Square

Surely there are some folks who will try to type "town" to go to the town square, but experience on my own PennMUSH games shows that they pretty quickly learn to just use the short names.  Omitting long exit names and aliases simplifies the building commands and the code.

## Exit Locks

Penn/Tiny exit locks could be infinitely complex.  You could lock an exit so it was only available to people whose name started with "B", or whose position was "Doctor", or even have a lock that was only opened on Tuesdays.

This functionality seems inordinately complex and pretty useless, so it has been ditched from Ares.  Standard exit locks operate based solely on [roles](/tutorials/manage/roles).  There's also a temporary lock feature for privacy that applies to interior locks.   A similar feature could be added for an apartment system, so only people on the lock list could get in.  

In short: Ares lets you create lock code for specific purposes, rather than attempting to design a super-flexible lock scripting language.

## Multiple Connections

"How do I boot my extra connection?" is a common refrain on MUSHes.  Zombie connections, reconnects - it's a pain in the butt.  Ares doesn't do any of that.  When you reconnect, it kills your old connection.

As a consequence, you can't leave yourself logged in from multiple places at the same time.  I understand some people use this feature so they won't miss anything while they're switching computers, but they are decidedly in the minority.  Allowing simultaneous connections adds a lot of complexity to the codebase (and to a lesser extent the player commands).

## Dolist

I can imagine the admins now:  "OMG HOW WILL I LIVE WITHOUT DOLIST?"   Dolist is a necessary evil on Penn and Tiny because of the way they're structured, but Ares is different.  Think about when you commonly use a dolist.  Need to teleport a bunch of people?  

    @dolist a b c=@tel ##=wherever

But why should that be necessary?  Wouldn't it be much easier if the teleport command just let you do that directly?

    tel a b c=wherever

Ares commands are designed to work on lists where it makes sense, eliminating the need for dolists.  At least, that's the theory.  If you find something missing, please provide [feebdack](/feedback).

## Darkness

You can't go dark on Ares.  Why not?  Because I find the idea of lurking admins to be creepy, and very big-brother-ish.

If you don't want to be bothered, there's a 'duty' command to mark yourself as off-duty.  You can also use the 'do not distrub' feature on pages.

## Force

In Ares, admins cannot force players to execute commands, mainly because I think it's creepy.  Admin-only commands should exist to do the things you need to do.  As with dolist, if you find something missing, just provide [feebdack](/feedback).

## Thing Objects

Ares has no "Thing" object type.  That means no rings, no notepads, no blaster pistols, no Viper fighter craft to climb into, etc.   Why?  All of those things are done in different ways.

Things that were cosmetic have been supplanted by a more robust 'detail' system.  If you want a special desc for your ring or the family photo on your wall, add a detail.

Things that were used for inventory tracking (weapons, armor, etc.) don't exist in the standard codebase because the standard codebase has no code that uses that sort of stuff.  FS3 Combat lets you select whatever weapons and armor you want, and leaves "should I have this" up to the player and combat organizer.   If you wanted to code a different system that kept track of what gear a player had, you'd create specific database fields to track the gear, not generic @created objects.

Things that stored code don't exist because Ares doesn't associate code with objects at all.  Code lives on the server.  There is no player-side code scripting.  Notepad and multi-descer code is built into the game as globals.

Things that were used as vehicles to drive around in don't exist because frankly I find them kind of silly.  If you really needed to model a vehicle or elevator or whatnot, you could utilize a room with movable exits and some custom code to do emits.

If you have trouble philosophically adapating an old-style MUSH system to Ares' Thing-less world, just [ask for help](/feedback).