---
title: Configuring the Achievements System
tags:
- config
layout: page
---

Achievements is an optional plugin that lets you set up in-game achievements for characters to earn.  To configure the Achievements plugin:

1. Select Admin -> Setup.
2. Edit `achievements.yml`

{% include toc.html %}

## types

You can configure what achievement types exist and what their icon is.  Standard types include things like community, story, and portal.  Icons come from the [Font Awesome](https://fontawesome.com/?from=io) icon library, so you'll see codes like `fa-globe` and `fa-users`.

{% tip %} 
Don't erase the existing types, because they're used by various plugins. You can change their icons.
{% endtip %}

## Defining Custom Achievements

Custom achievements must be defined in a plugin's configuration file.

Some plugins already have some. For example, in the `forum.yml` config file, we define the forum-related achievements:

(Under the config setting 'achievements')

      forum_reply:
        type: community
        message: Replied to a forum post.
      forum_post:
        type: community
        message: Created a forum post.

You can add to one of these lists. If it doesn't fit into an existing plugin achievement list, you can edit use the one in `achievements.yml`.

(Under the config setting 'achievements')

        player_of_the_month:
          type: social
          message: Recognized as Player of the Month.

{% tip %}
The achievement key (e.g., `player_of_the_month` or `forum_reply`) is just a code name. It's not showed to players and should not contain special characters other than underscores.
{% endtip %}

### Adding Achievements To New Plugins

If you are making a new plugin, or adding achievements to a plugin that doesn't already have them, you'll need to _register_ those achievements with the plugin manager.  This is done by defining a `self.achievements` method in your plugin definition.

For example, in `aresmush/plugins/forum.rb`:

    def self.achievements
      Global.read_config('forum', 'achievements')
    end

## Awarding Achievements In Code

Once a new achievement is defined, you can use the `achievement/add` command to award it to someone.

If you want some piece of code to award a custom achievement automatically, just call: `Achievements.award_achievement(char, achievement_name)`.  For example:

    Achievements.award_achievement(char, "player_of_the_month")

{% tip %} 
You don't have to check to see if the person already has the award; the Achievements plugin does that automatically.
{% endtip %}

## Multi-Level Achievements

Some achievements can be earned more than once at different levels.  For instance, the `scene_participant` achievement is "Participated in XXX scenes", and is awarded at various scene thresholds (1, 10, etc.)

To avoid spamming the config list with the same achievement named differently (scene_participant_1, scene_participant_10, etc.), you can instead track a _count_ along with the achievement.  There are three pieces to this:

* In the achievement definition, add a `levels` option defining the valid count thresholds.
* In the achievement message, use `%{count}` where you want the count to be shown.  For example:  "Wrote %{count} words in scenes."
* When you award the achievement, specify how many things the user **currently** has. The code will figure out if they've met the threshold to get the next level award.  `Achievements.award_achievement(char, "word_count", 1242)`
 
For examples:

    scenes:
      achievements:
        word_count:
          type: story
          message: Wrote %{count} words in scenes.
          levels:
          - 1000
          - 2000
          - 5000
          ...