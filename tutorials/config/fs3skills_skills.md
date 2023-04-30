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

## Changing an Existing Ability

If you want to remove, rename, or change the category of an existing ability (e.g., moving it from Action Skill to Background Skill or vice-versa), you will either need to:

1. Make sure no existing character has that ability.
2. Use a code tinker to update existing abilities behind the scenes.

You'll also need to update any chargen or combat configuration that references that ability (e.g., a weapon skill or CG starting skill).

If you remove, rename, or change a skill category when characters *already* have that ability on their sheets, you will cause errors. Characters may not be able to change/remove the modified skills, or you might get configuration errors such as:

    Error: "Error in skills configuration -- action skill Archery not found."

To avoid these problems, you will need to fix everyone's character sheet. 

* If you are just **removing** an ability, use the `wipeability <name>` admin command.
* If you are just **renaming** an ability, use the `renameability <old name>=<new name>` admin command.
* If you want the nuclear option, just have everyone do `reset` in chargen to clear all their abilities and start fresh.
  
If you need more advanced handling - like refunding XP, or changing skill categories - you will need to use a custom [Tinker snippet](/tutorials/code/tinker.html) to update everyone's sheets. For example, if you wanted to do something for everyone who had the "Archery" action skill:

```
def handle
  FS3ActionSkill.all.each do |ability|
     if (ability.name == 'Archery')
       # Your code goes here
     end
  end
end
```

Don't be shy to [ask for help](/feedback.html) if you need to.