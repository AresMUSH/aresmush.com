---
title: Custom Code Hooks
description: 
layout: page
tags:
- code
- features
---

Normally, modifying the base Ares code exposes you to *merge conflicts*.  This is an annoying process that forces you to reconcile your changes with the base code changes whenever you upgrade.

There are, however, several places that are designed with **custom code hooks**, which let you hook in custom code without actually touching the core code.

{% include toc.html %}

## Chargen Hooks

* [Chargen App Review](/tutorials/code/hooks/app-review.html) - Character fields checked on the app review screen, like making sure their groups make sense or a custom chargen field is set.
* [Chargen Approval Triggers](/tutorials/code/hooks/approval-triggers.html) - Actions taken after approval, like assigning roles or adding characters to channels based on their groups.
* [IC Starting Location](/tutorials/code/hooks/starting-location.html) - If you want people from different factions/homeworlds/etc. to start in different places, you can use the custom IC starting location hook.
* [Character Fields](/tutorials/code/hooks/char-fields.html) - New character fields added to profiles and/or chargen.

## Scene Hooks

* [Scene Buttons](/tutorials/code/hooks/scene-buttons.html) - Actions added to the Play menu or pose buttons on active scenes.
* [Character Cards](/tutorials/code/hooks/char-cards.html) - Custom appearance for the mini character profiles that show up during active scenes when you select a character's icon.

## Job Hooks

* [Custom Job Menu](/tutorials/code/hooks/job-menu.html) - Adding custom job menu actions.

## FS3 Combat Hooks

* [Combat Actions](/tutorials/code/hooks/fs3-actions.html) - Adding new combat actions to FS3.
* [New Turn Triggers](/tutorials/code/hooks/fs3-new-turn.html) - Actions to be taken at the end of each turn, like resetting flags or handling special kinds of damage.

## Web Portal Hooks

* [Custom Routes](/tutorials/code/hooks/custom-routes.html) - Adding custom routes (pages) to the web portal.

