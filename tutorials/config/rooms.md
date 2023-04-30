---
title: Configuring the Rooms System
layout: page
tags:
- config
---

To configure the Rooms plugin:

1. Select Admin -> Setup.
2. Edit `rooms.yml`

{% include toc.html %}

## area_directory_order

In the locations directory, top-level areas are displayed in alphabetical order by default. You can override that by listing your desired order. Any areas not listed will be placed in alphabetical order. 

For example, if your areas are A, B, C, D, E and your config was: `[ "D", "B" ]` then D and B would be first followed by A, C, and E in alphabetical order. Alternately, you could list all the areas: `[ "D", "B", "C", "E", "A" ]`.

## area_display_sections 

This option controls whether each top-level area in the web portal locations directory gets its own row/header. You probably want to set this to false if you don't have nested areas.

## icon_types

You can assign icons to rooms so they show up highlighted on the locations directory. By default, a 'star' icon is available to designated featured hangouts. You can expand this with additional icon types if desired, to distinguish bars, parks, etc. Just give each icon type a name and a [Font Awesome](https://fontawesome.com/?from=io) icon code.

## room_lock_cron

The game will periodically unlock empty interior rooms that have been temporarily locked (like residences and RP rooms).  It does not affect rooms that have a permanent role lock.  You may want to turn this off if you view room locks as more of an IC thing (i.e. characters shouldn't enter because the room is ICly locked) as opposed to an OOC lock for scene privacy.

There is a cron job to control when this happens.  By default it does this every hour.  See the [Cron Job Tutorial](http://www.aresmush.com/tutorials/code/cron.html) for help if you want to change this.
