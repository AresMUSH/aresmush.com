---
title: Configuring FS3 - Chargen
layout: page
tags:
- config
---

To configure the FS3 Chargen Limits:

1. Select Admin -> Setup.
2. Edit `fs3skills_chargen.yml`

{% include toc.html %}

## Before You Start

You should read the article [Customizing FS3](http://aresmush.com/fs3/fs3-3/tweaking-fs3.html), which contains important information to help guide you in customizing your game.

{% note %} 
Many of the chargen configuration options are lists.  They can't be left blank.  If the list is empty, use `[]` to reflect an empty list.
{% endnote %}

## free_languages and free_backgrounds

The first few points in Language and Background Skills are free, meaning they do not count toward a character's Ability Point total.  

* **free_languages**: Free points in Language Skills.  Make sure you assign 3 (Fluent) for each of the starting languages you set up in the skill list.
* **free_backgrounds**: Free points in Background Skills.

## min_backgrounds

You can require how many Background Skills (distinct skills, not points) a character must start with.

## advantages_cost

If you are using Advantages, you can configure the cost.  The default is 2 points per dot.  You can adjust this depending on how valuable advantages are in your game.  Making different advantages cost different amounts will require custom code.

## max_skill_rating and max_attr_rating

FS3 Attributes are rated from 1-4 (with 4 being Exceptional) and Skills are rated from 1-8 (with 8 being Legendary).  Some games may want to limit the maximum starting rating by setting these values lower than the default.

Two important notes:

- No matter what you set this to, the system doesn't support ratings above 4 for attributes or 8 for skills.
- This limit applies only to Chargen.  For XP limits, use the [XP configuration](/tutorials/config/fs3skills_xp.html).

## allow_incapable_action_skills

The Incapable level might not be necessary in every setting.  See [Everyman vs. Incapable](/fs3/fs3-3/chargen.html#unskilled) for details.  To avoid confusion in chargen, the 'Incapable' level is disabled by default.  You can enable it by setting this setting to true.

## Guiding Maximums

You can configure various guidelines about what skills and attributes a character can have. 

{% note %} 
These are soft limits.  The system will let someone go over them, but a warning will appear in their app command status.  You can choose whether to allow a special exception when approving the character.
{% endnote %}

### max_ap

This is the maximum Ability Points a character can spend.  Free skills and attributes don't count toward this total.

### max_points_on_attrs, max_points_on_action, and max_points_on_advantages

This is the maximum number of chargen points a character can spend on attributes, action skills and advantages.  Ratings 1-2 (for attributes) and 1 (for action skills) are **not** counted towards the total.  

Attributes cost 2 points per dot and skills cost 1 point per dot.  For example - setting `max_points_on_attrs` to 10 would allow you to buy 5 attribute dots above level 2.  The cost for advantages is configurable.

Note: These limits also apply to XP spent after chargen, unless modified by the XP settings (see [Configuring FS3 XP](/tutorials/config/fs3skills_xp.html)).

### max_skills_at_or_above and max_attrs_at_or_above

You can set break points for attributes and skills to limit how many a character can have at or above a given level. 

    max_skills_at_or_above:
        6: 2
        7: 1
    
    max_attrs_at_or_above: 
        4: 2
        5: 1

Remember that these limits are at *or above*.  So given the max skills example above:

> 1 at 6, 1 at 7 --> OK
>
> 2 at 6 --> OK
>
> 2 at 7 --> *NOT* OK  (even though you can have 2 above 6, only 1 of them may be at or above 7)
>
> 2 at 6, 1 at 7 --> *NOT* OK (you can only have 2 skills total at or above 6)

## starting_skills

FS3 lets you assign starting skills and specialties for different groups.  For example, you may want to ensure that people from a certain colony all start with a particular language, or that people in a certain position start with certain professional skills. As with the rating limits, these are soft targets.  The app command status will have a warning if any starting skills are missing or too low.

{% tip %} 
Despite the word 'skills' in the name, you can also include attributes, languages, and advantages under `skills`.
{% endtip %}

{% tip %} 
Make sure you allocate enough free language points in chargen to cover rating 3 (Fluent) in each starting language, otherwise the languages will count towards a character's Ability Point total.
{% endtip %}

### Group Skills

Starting skills are group-based, so you'll see multiple entries for different groups in the list.  You can list skills and also specialties.  Here is an example:

    Faction:
        Navy:
            skills:
                Swimming: 2
        Marines:
            skills:
                Melee: 2
                Brawn: 3
    Position:
        Pilot:
            skills:
                Piloting: 3
            specialties:
                Piloting:
                    - Viper
                    - Raptor
        Rifleman:
            skills:
                Firearms: 3
                Melee: 3

A Navy Pilot would start with Swimming: 2 and Piloting: 3, whereas a Marine Pilot would start with Melee: 2 and Piloting: 3.  The system will take the highest rating out of all applicable groups, so a Marine Rifleman would start with Melee: 3 and Firearms: 3.

### Everyone Skills

Sometimes you may want to give a skill to everybody.  Instead of duplicating the information in each group, you can use the special "Everyone" group.  For example, to make everyone start with Alertness 2 and fluent English:

    Everyone:
        skills:
            Alertness: 2
            English: 3

{% tip %} 
You probably want to make sure everyone starts out as fluent (3) in whatever the game's common language is.
{% endtip %}

## unusual_skills

You can mark certain skills as unusual in your setting.  Characters with those skills above Fair will receive a warning prompting them to have a good reason.

    - Celtan
    - Demolitions