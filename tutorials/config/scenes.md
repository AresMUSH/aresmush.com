---
title: Configuring the Scenes System
layout: page
tags:
- config
---

To configure the Scenes plugin:

1. Select Admin -> Setup.
2. Edit `scenes.yml`

{% include toc.html %}

## scene_types

You can configure the available scene types.  By default they are "event", "social" and "vignette".  This helps categorize logs on the Web Portal.

## ooc_color

You can configure the color that is used in OOC asides. You can use multiple color codes.  For example: %xh%xc

## room_cleanup_cron

The game will periodically clear scene sets and scenes from empty rooms.  

There is a cron job to control when this happens.  See the [Cron Job Tutorial](http://www.aresmush.com/tutorials/code/cron.html) for help if you want to change this.

{% note %} 
Scenes in temp rooms will remain open as long as there are characters still in the room - even if they're logged off.  Scenes in grid rooms will stop after everyone logs off.
{% endnote %}

## include_pose_separator

When you complete a scene and share the log, the default behavior is to compress all the poses together into a single narrative, like you'd find in a book.  You can alternately include a separator line between poses to make it more clear which pargarphs went together in a single pose.  This separator can be styled with custom CSS using the 'pose-divider' class.

## idle_scene_timeout_days

Scenes in grid rooms are automatically closed when there's nobody left in the room.  Scenes in temp rooms (including scenes played solely on the web portal) are closed after this many days without activity.


## trending_scenes_cron and trending_scenes_category

The game will post trending scenes (i.e. recent scenes with the most 'likes' on the web portal) to a forum.  By default this happens once a week, and you can control the timing with `trending_scenes_cron`.  You can also control which forum it posts to with `trending_scenes_category`.  Leave the category blank to disable the post.

## use_custom_char_cards

Character cards are mini-profiles that are shown when you click on a character's icon next to their pose. If you enable this setting, the game will use your own custom code for the character cards instead of the built-in ones.  See [Custom Character Cards](/tutorials/code/hooks/char-cards.html).

## related_scenes_filter_days

The 'related scenes' dropdown doesn't show ALL scenes for performance reasons.  It will only show scenes that have been shared within a certain number of days.  You can configure that limit.  Be careful about making it too large, as that can lead to lag when editing scenes.


## content_warnings

This is a list of pre-made content warnings that players can choose from the list when creating a scene. They can still enter their own no matter what you put here; this list just provides guidance for what sorts of things they should consider warning about.


## Deleting Unshared Scenes

The game is not designed to store unshared scenes indefinitely. This can lead to memory bloat, game lag, and performance issues. There are several ways unshared scenes can be marked for deletion:

* Manually by a player or admin using the scene/delete command or web menu item.
* Automatically by the unshared scene cleanup feature. (optional)
* When a player idles out. Usually relevant for roster games that may not want new roster players to inherit private scenes from the old player. (optional)

{% note %}
In all cases, scenes are only deleted immediately if there have never been any poses. If any poses exist, there will be a grace period and notification so participating players can download, share, or restart the scene before it's deleted.
{% endnote %}

There are several configuration options related to these features:

### delete_unshared_scenes
Turns the automatic unshared scene cleanup feature on or off.

{% warning %}
Disabling this can lead to memory bloat, game lag, and performance issues.
{% endwarning %}

### unshared_scene_warning_days

If `delete_unshared_scenes` is enabled, this is how long completed scenes can remain unshared before they are marked for deletion. This doesn't include the grace period before the scene is actually deleted - that's controlled by `scene_trash_timeout_days`.

### scene_trash_timeout_days

When a scene is marked for deletion (either manually or automatically), this option controls the grace period before the scene is actually deleted. It may not be set lower than 14 days.

### delete_scenes_on_idle_out

Whether unshared scenes should be marked for deletion when a participating character idles out. The usual grace period still applies before the scene actually gets deleted.

### unshared_scene_cleanup_cron

See the [Cron Job Tutorial](http://www.aresmush.com/tutorials/code/cron.html) for help if you want to change when the cron job runs. Don't use this to turn the feature on or off - use `delete_unshared_scenes` instead.

## Custom Scene Pose Buttons

Below the pose editor in a live scene is a row of buttons including "Add Pose" and "Add OOC".  With custom code, you can add custom buttons here that make use of the contents of the scene pose window--for instance, for sending a text message. See [Custom Scene Buttons](/tutorials/code/hooks/scene-buttons.html).

## Custom Scene Menu Buttons

You can also add new menu items to the live scene's "Play" menu with custom code. You might do this if you're designing a new "extra" for a skill system, for instance.  See [Custom Scene Buttons](/tutorials/code/hooks/scene-buttons.html).

