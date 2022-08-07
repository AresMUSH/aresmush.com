---
title: Removing a Database Field
description: 
layout: page
tags:
- code
- database
---

Ares uses the [Ohm](http://ohm.keyvalue.org/) database library to access fields in the Redis database.  Adding new fields to Ohm database models is very easy.  Removing them requires a little more work.

{% include toc.html %}

## Why Removing is Tricky

For example - let's say that you had an attribute named favorite_color on the Character class:

    class Character < Ohm::Model
      attribute :name
      attribute :favorite_color
    end

You make some code to set it, and now some characters have a favorite color.  

Now you've decided you don't need favorite color after all.  You remove it from the class.  Everything seems fine, but then you start seeing all kinds of warning messages in the logs:

    WARN - Model AresMUSH::Character failed to respond to favorite_color undefined method `favorite_color='

This is happening because you've got data for `favorite_color` in the databse, but nowhere to put it on the Character object!   Ohm assumes that's a coding mistake and gives you a warning.

## Removing Fields Safely

To prevent this from happening, you should set all instances of the field to `nil` in the database **before** removing it from the code.

{% note %} 
If the field was originally a special data type (like DateTime or Integer) we need to change it to a string data type first by removing the `type` specification.  Otherwise our nil may be converted to a default value (like 0).
{% endnote %}

For example, assume we have:

    class Character < Ohm::Model
      attribute :favorite_number, :type => DataType::Integer
    end

First we would change the field to a string attribute and then reload the affected plugin:

    class Character < Ohm::Model
      attribute :favorite_number
    end

Then we can use a [tinker](/tutorials/code/tinker.html) command to reset everyone's colors:

    def handle
      Character.all.each { |c| c.update(favorite_number: nil) }
    end

Now it's safe to remove the field from the code.

{% tip %} 
If you forgot to nil out the field before you removed it from the code, just put it back temporarily.  Run the commands above, then remove it for real.
{% endtip %}

## Errors During Restart

Sometimes you'll get in a jam when you've shut down the game and it won't restart due to the database error.  You can't use tinker to fix the problem because you can't get onto the game!

When this happens, you can use a database script to help you.

1. Edit the file `aresmush/install/scripts/remove_db_field.rb` to add back the field temporarily and clear it out. The code is basically the same as what you would have used in the tinker example above.  There's some sample code in the file you can modify.
2. Run the script using `bin/script remove_db_field`.
3. Restart the game.

## Errors After Upgrades

If you get these errors after a code upgrade, it's likely that you just forgot to run a database migration during a [code upgrade](/tutorials/manage/upgrades.html).
