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

### Big Bads

Some games try to have a "big bad" type of NPC level with dice pools of 15+.  However, giving somebody a ton of dice to roll does NOT make them unstoppable by any stretch.  Many a game has thought they had a "Big Bad" beastie ready to give the PCs a hard time, only to have it felled in a single turn.  The numbers *just don't scale* for beyond-human abilities.

### default

The default rating is what the NPC rolls for skills by default.

{% tip %} 
This is a total dice pool, encompassing skill plus attribute.  So if you want a boss to be equivalent to an "Expert" PC with a "Good" attribute, you need to give them a die pool of 9 (6+3).
{% endtip %}

    Goon:
        Default: 4
    Henchman:
        Default: 6
    Boss:
        Default: 8

{% note %} 
When the system needs an attribute (e.g., Brawn or Reflexes), it will use **half** the default rating. So a Goon in the above example would have a Brawn of 2.
{% endnote %}

### Fine-Tuning Skills

You can also fine-tune dice pools for specific skills.  This is helpful if you want to make a Boss tough to take down without making them extraordinarily deadly (or vice-versa).  You can also make specialist NPCs who are good with some weapons but not others.

    Goon:
        Default: 4
        Firearms: 6
        Gunnery: 6
        Piloting: 4
    Henchman:
        Default: 6
        Firearms: 8
        Gunnery: 8

Any skills not expressly listed will use the 'Default' value.

### wounds

Finally, there is a setting for 'Wounds' which is a lethality bonus (or penalty) added to all damage they **take**. To make goons easier to damage and bosses harder, you could do:

    Goon:
        Default: 4
        Wounds: 30
    Boss:
        Default: 6
        Wounds: -10

## default_npc_type

You can set what the default NPC type is.  It must be one of those specified in the `npc_types` list.