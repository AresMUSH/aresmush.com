---
title: Configuring FS3 Combat - Armor
layout: page
tags:
- config
---

To configure the FS3 armor types:

1. Select Admin -> Setup.
2. Edit `fs3combat_armor.yml`

{% include toc.html %}

## Before You Start

Read **[How Armor Works](http://aresmush.com/fs3/fs3-3/combat-mechanics.html#armor)** to understand how the armor mechanic works in FS3.

{% tip %}
You should use the `gear/check` command after changing the FS3 gear configuration.  It will warn you about several common *possible* configuration problems.  You can review them to see if they're intentional or not.  It doesn't catch everything, though.
{% endtip %}

## Armor Types

You can define as many kinds of armor as you want.  FS3 armor types have the following stats, explained below:

    Police:
        description: Light ballistic vest.
        protection: 
            Chest: 6 
            Abdomen: 5
        defense: 0

### Description

The description is just ree-form text describing the armor.  It's best to use double quotes around it.

### Protection Values

You can specify different protection values for different locations, making weak spots or skipping areas that are completely uncovered. For example, the simple kevlar vest shown in the example above protects the chest and abdomen but nowhere else.  It protects the chest slightly more due to the heart-protector plate.

{% note %}
Any hit location not listed will have a protection of 0, meaning no armor. That means for a vest, for example, you only need to list chest and abdomen.
{% endnote %}

### Defense

Armor can impact defense compared to an un-armored person.  Clunky platemail might give a defense penalty, while agile power armor might give a defense bonus.

## Armor Specials

Like weapon specials, armor specials allow you to define 'extras' that can augment armor.  Common specials might be helmets or shields.  

Specials can provide a bonus or penalty (if the value is negative) to protection or defense.  This value is added to the armor's base value.  In the examples below, a helmet provides armor to the head while a shield provides armor to the arm and a defense bonus.

    Helmet:
        description: "A helmet"
        protection:
            Head: 4
    
    Shield:
        description: "Simpler buckler."
        defense: 2
        protection:
            Right Arm: 2


## Vehicle Armor

Vehicles can have armor.  It works the same way as personal armor, but it is automatically 'worn' by the vehicle; you don't have to use a separate command to apply it.