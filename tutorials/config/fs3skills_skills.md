---
title: Configuring FS3 - Skills List
layout: page
tags:
- config
---

To configure the FS3 Skills List:

1. Select Admin -> Setup.
2. Edit `fs3skills_action.yml`, `fs3skills_attrs.yml`, `fs3skills_bg.yml`, `fs3skills_langs.yml` and `fs3skills_advantages.yml`.

{% include toc.html %}

## Before You Start

You should read the article [Customizing FS3](http://aresmush.com/fs3/fs3-3/tweaking-fs3.html), which contains important information to help guide you in customizing your game.

## Attributes

You can configure the list of Attributes, specifying a name and description for each.

    - name: Reflexes
      desc: 'Reflexes, dexterity, and hand-eye coordination.'
    - name: Brawn
      desc: Physical strength and toughness.

### default_linked_attr

This is the Attribute used by default when someone rolls a Background or Language skill and doesn't specify an Attribute.  For example, if you set this to 'Wits' then someone rolling Basketweaving will really be rolling 'Basketweaving+Wits'.

{% note %} 
This only applies to Background and Language Skills.  Action Skills all specifiy their own linked Attribute.
{% endnote %}

## attributes_blurb

This is the instructional blurb used in the abilities screen and in chargen help.  It supports markdown text.

## Action Skills

You can configure the list of Action Skills, specifying a name, description and linked Attribute for each.

    - name: Alertness
      desc: Noticing things and being aware of your surroundings.
      linked_attr: Perception
    - name: Athletics
      desc: General running, jumping, climbing, etc.
      linked_attr: Brawn

You may optionally specify a list of specialties for a skill.

    - name: Medicine
      desc: Tending to the ill and injured.
      linked_attr: Wits
      specialties:
      - Doctor
      - Surgeon

## action_skills_blurb

This is the instructional blurb used in the abilities screen and in chargen help.  It supports markdown text.

## Languages

You can configure the list of Languages, specifying a name and description for each.

    - name: Standard
      desc: Spoken across the colonies.
    - name: Gemenese
      desc: Dead language known by academics and religious scholars.

### language_blurb

This is the instructional blurb used in the abilities screen and in chargen help.  It supports markdown text.

## Advantages

Advantages are an optional part of the system.  You can use them for things that aren't skills, but that you want people to pay points for in chargen - rank, resources, powers, etc.  

{% note %}
Advantages are more akin to the old Storyteller system Backgrounds than they are to things like CofD merits/flaws, Cortex assets/complications, or Shadowrun positive/negative qualities.  You can't have different costs/limits for different advantages.  They're all rated 1-3 and they all cost the same.

They basically work exactly like background skills, but they're in a separate category because they're... not skills.
{% endnote %}

You can configure the list of Advantages, specifying a name and description for each.

    - name: Resources
      desc: Wealth and other tangible possessions.
    - name: Rank
      desc: Rank or social status.

### use_advantages

You can disable Advantages entirely by setting `use_advantages` to false.  This is the default setting.

### advantages_blurb

This is the instructional blurb used in the abilities screen and in chargen help.  It supports markdown text.

## Removing an Ability

If you remove an Action Skill, Attribute or Language from the game configuration while people have that ability, you'll get errors or weird results.

    Error: "Error in skills configuration -- action skill Archery not found."

If your game is still in development and you've just got characters in chargen, having them do a 'reset' to wipe their abilities will fix this.

Otherwise, **before** removing an ability from the game configuration, you must first run a [Tinker snippet](/tutorials/code/tinker.html) to remove that ability everyone's character sheet.  You can also do special handling, like refunding them some XP or transferring it to a background skill or something.  

For example, if we wanted to remove the Archery action skill, we would modify the tinker command to do:

      def handle
        FS3ActionSkill.all.each do |a|
           if (a.name == 'Archery')
             client.emit "Deleting Archery from #{a.character.name} -- was at rating #{a.rating}."
             a.delete
           end
        end
      end

After you have successfully removed the ability from everyone's sheet, *then* it is safe to remove the ability from the config file.