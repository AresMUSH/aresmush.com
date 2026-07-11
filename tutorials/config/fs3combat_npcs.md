---
title: Configuring FS3 Combat - NPC Skills
layout: page
tags:
- config
---

You can configure the skill levels used by NPCs in FS3 combat.

1. Select Admin -> Setup.
2. Edit `fs3combat_npcs.yml`

{% include toc.html %}

## npc_types

You can define the NPC types available in your game.  The standard ones are Goon, Henchman, Miniboss and Boss.

{% tip %}
These NPC types **only have meaning in combat**. Outside of combat, NPC skill rolls are freeform and you have to manually specify how many dice they're rolling.
{% endtip %}

### default

The default rating is what the NPC rolls for skills.

{% note %} 
This is a **total** dice pool, encompassing skill plus attribute. If rolling an attribute by itself, it uses **half** the default value.
{% endnote %}

    Goon:
        Default: 4
    Henchman:
        Default: 6
    Boss:
        Default: 8

For example, Goon is tuned for average attr (2) + fair skill (2) = 4 dice total. If you want a boss to be equivalent to an "Expert" PC with a "Good" attribute, you need to give them a die pool of 9 (6+3). 

### Fine-Tuning Skills

You can also fine-tune dice pools for specific abilities.  This is helpful if you want to make a Boss tough to take down without making them extraordinarily deadly (or vice-versa).  You can also make specialist NPCs who are good with some weapons but not others.

{% tip %} 
For skills, the listed number is a **total** dice pool, encompassing skill plus attribute.
{% endtip %}

    Goon:
        Default: 4
        Firearms: 6
        Gunnery: 6
        Piloting: 4
    Henchman:
        Default: 6
        Firearms: 8
        Gunnery: 8

Any skills not expressly listed will use the 'Default' value, so it's not necessary to exhaustively list every ability.

If you list an attribute by itself, it is used for attribute-only rolls but will NOT affect the other skill ratings. For example, the following henchman config will roll 4 dice for dodging (Reflexes only), but only 8 dice for Firearms+Reflexes.

    Henchman:
        Default: 6
        Firearms: 8
        Gunnery: 8
        Reflexes: 4

### wounds

Finally, there is a setting for 'Wounds' which is a lethality bonus (or penalty) added to all damage they **take**. To make goons easier to damage and bosses harder, you could do:

    Goon:
        Default: 4
        Wounds: 30
    Boss:
        Default: 6
        Wounds: -10

### Big Bads

Some games try to have a "big bad" type of NPC level with dice pools of 15+.  However, giving somebody a ton of dice to roll does NOT make them unstoppable by any stretch.  Many a game has thought they had a "Big Bad" beastie ready to give the PCs a hard time, only to have it felled in a single turn.  The numbers *just don't scale* for beyond-human abilities. This is a [dev blog post]({{site.baseurl}}/blog/scaling-in-fs3.html) if you want more details.

## default_npc_type

You can set what the default NPC type is.  It must be one of those specified in the `npc_types` list.