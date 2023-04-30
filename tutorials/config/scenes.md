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

## delete_unshared_scenes

There's also another cron job to periodically delete scenes that have been completed but not shared.  It also warns people about unshared scenes that are going to be deleted soon.  You can turn this feature on and off by setting `delete_unshared_scenes` to true or false.

{% warning %}
Disabling the unshared scene cleanup (or configuring the timeout too long) can cause memory bloat, especially on larger games. This can lead to game lag unless you increase your droplet RAM size to keep pace with the number of shared scenes.
{% endwarning %}

If it's set to true, there are a few other things you can configure:

### unshared_scene_cleanup_cron

See the [Cron Job Tutorial](http://www.aresmush.com/tutorials/code/cron.html) for help if you want to change this.

### unshared_scene_deletion_days and unshared_scene_warning_days

You can configure how long to wait before deleting unshared scenes.  For example:

    unshared_scene_deletion_days: 20
    unshared_scene_warning_days: 13

Whenever the unshared scene cron job runs, it will warn participants in unshared scenes that were completed more than 13 days ago.  It will delete unshared scenes that were completed more than 20 days ago - effectively giving a 7-day grace period after the warning.

## trending_scenes_cron and trending_scenes_category

The game will post trending scenes (i.e. recent scenes with the most 'likes' on the web portal) to a forum.  By default this happens once a week, and you can control the timing with `trending_scenes_cron`.  You can also control which forum it posts to with `trending_scenes_category`.  Leave the category blank to disable the post.

## use_custom_char_cards

Character cards are mini-profiles that are shown when you click on a character's icon next to their pose. If you enable this setting, the game will use your own custom code for the character cards instead of the built-in ones.  See [Custom Character Cards](/tutorials/code/hooks/char-cards.html).

## related_scenes_filter_days

The 'related scenes' dropdown doesn't show ALL scenes for performance reasons.  It will only show scenes that have been shared within a certain number of days.  You can configure that limit.

## content_warnings

This is a list of pre-made content warnings that players can choose from the list when creating a scene. They can still enter their own no matter what you put here; this list just provides guidance for what sorts of things they should consider warning about.

## Custom Scene Pose Buttons

Below the pose editor in a live scene is a row of buttons including "Add Pose" and "Add OOC".  With custom code, you can add custom buttons here that make use of the contents of the scene pose window--for instance, for sending a text message. See [Custom Scene Buttons](/tutorials/code/hooks/scene-buttons.html).

## Custom Scene Menu Buttons

You can also add new menu items to the live scene's "Play" menu with custom code. You might do this if you're designing a new "extra" for a skill system, for instance.  See [Custom Scene Buttons](/tutorials/code/hooks/scene-buttons.html).

