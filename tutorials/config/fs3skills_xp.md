---
title: Configuring FS3 - Experience
layout: page
tags:
- config
---

To configure the FS3 Skills List:

1. Select Admin -> Setup.
2. Edit `fs3skills_xp.yml`

{% include toc.html %}

## Before You Start

You should read the article [Customizing FS3](http://aresmush.com/fs3/fs3-3/tweaking-fs3.html), which contains important information to help guide you in customizing your game.

## periodic_xp

This is the amount of XP that is given out each time the periodic cron job runs (weekly by default).

## max_xp_hoard

You can configure the maximum amount of XP that someone can save up.  The default gives people a little buffer in case they forget to spend their XP, but keeps them from raising a flurry of skills all at once.

## days_between_learning

This is essentially a 'cooldown' between XP spends on a specific skill.

## attr_dots_beyond_chargen_max, action_dots_beyond_chargen_max and advantage_dots_beyond_chargen_max

The [chargen limits](/tutorials/config/fs3skills_chargen.html) of `max_points_on_attrs`, `max_points_on_action` and `max_points_on_advantages` are still in effect after chargen, controlling how far characters can raise their abilities above average.  This prevents the dinosaur effect where someone can become awesome at everything given enough time.  It keeps veteran characters from getting too far ahead of new characters.

Even so, you may want to allow someone who started at the chargen max to have a little room to grow.  The settings `attr_dots_beyond_chargen_max`, `action_dots_beyond_chargen_max` and `advantage_dots_beyond_chargen_max` are _added to_ the chargen maximums to control the absolute maximums that characters can achieve with XP.

For example:  Let's say your game has 6 attributes, `max_points_on_attrs` set to 12, and `attr_dots_beyond_chargen_max` set to 3.

* Everyone gets rating 2 (average) for free.  That's 12 dots.
* They can buy *up to* 12 points (6 dots) more in chargen.  That's a max of 18 dots.
* They can buy up to 3 more dots *beyond that* with XP.  That's a max of 21 dots.

Notice that these are absolute limits.  Someone who starts off lower will have more room to grow than someone who started with the max at chargen.  

## allow_advantages_xp

This setting controls whether you can raise advantages directly with XP.  In some games they may be fixed at chargen and only alterable through plots.  In other games they may require special approval.  Set this to 'true' if you want to allow them to be learned just like any other ability.

## xp_costs

XP in Third Edition works a little differently than you might be used to.  Instead of saving up a ton of XP and spending them all at once, you spend them a little bit at a time to represent improvement over time.  There is a "cooldown" between XP spends on a single skill.

{% tip %} 
High skills take a long time to improve, but since you earn XP each week, you still have extra to spread around on other abilities while you're waiting.
{% endtip %}

When you have spent the total number of XP needed for the new ability rating, your rating rises.  

### Costs for First Rating

The first rating point (e.g. "Everyman" or "Interest") always costs 1XP and raises immediately.  **You cannot change this.**


### Costs for Subsequent Ratings

You can configure how many XP are needed for subsequent ratings after the first. The format is:

    ability_type:
      current rating: cost
      current rating: cost
    

For example:

    language:
        1: 4
        2: 12
  
Raising a Language from 1 (Beginner) to 2 (Conversational) costs 4 XP and going from 2 (Conversational) to 3 (Fluent) costs 12 XP.  Assuming a 1-month cooldown between raises, it will take 4 months to become Conversational and 12 to become Fluent.


Here's another example:

        action:
            1: 1
            2: 2
            ... etc.


Raising an Action Skill in that example is much easier.  It takes only 1 XP to go from 1 (Everyman) to 2 (Fair) and 2 XP to go from 2 (Fair) to 3 (Competent).  After that, though, the costs go up rapidly.  

### XP Skill Caps

If you don't want folks to advance beyond a certain skill level with XP, simply omit subsequent ratings from the costs chart.  For example:

        action:
            ...
            4: 6
            5: 8

Since there are entries for 6 and 7 in the table, you can't advance beyond level 6 using XP alone. It would require a staff member to manually assign the skill.

## xp_cron

The game will periodically award all approved/active characters XP.  By default this happens weekly on Saturday evenings.  See the [Cron Job Tutorial](http://www.aresmush.com/tutorials/code/cron.html) for help if you want to change this.
