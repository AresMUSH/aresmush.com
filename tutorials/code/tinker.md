---
title: Tinkering With Code
description: 
layout: page
tags:
- code
- tinker
---

Ares doesn't allow you to alter the game code from the MU client window, but sometimes you need to do things that aren't covered by an existing command - find all characters over 30 years old, update the faction on a bunch of people at once, etc.  There's no need to create specific commands for this sort of tinkering, especially if you're unlikely to do that specific task ever again.  In Ares, you can use the `ruby` command to execute simple code blocks, or the `tinker` command to perform more involved processing.

{% tip %} 
Not all admins can use the tinker/ruby commands - only characters with the  `coder`  role.  This is a security feature, because giving someone access to run arbitrary code essentially gives them the keys to the kingdom.  They could do literally anything with the database.
{% endtip %}

{% include toc.html %}

## Using the Ruby Command

The `ruby` command lets you run simple Ruby code snippets straight from your MU client.  Separate multiple lines with semicolons.  For example:

    ruby c = Character.find_one_by_name("Faraday");c.update_demographic("hair","blonde") 

## How to Tinker

Doing a lot of code on a single line can be cumbersome.  That's where the `tinker` command comes in.  Tinker is a built-in command that does nothing by default.  You update the command code to do whatever you need at that moment.  Unlike other commands, the tinker code can be easily updated through the web portal.

Tinkering involves three steps:

1. Log into the Web Portal with a coder character and select Code -> Tinker.  
2. Edit the code to do what you want and save it.
3. Type `tinker` in-game to run the code.

{% tip %} 
Coders who prefer to edit code in the server shell can edit  `aresmush/plugins/tinker/commands/tinker_cmd.rb`  then reload the code using  `load tinker`  in-game.
{% endtip %}

## Tinkering Examples

Let's say you wanted to write a quick code snippet to find all the characters who are 30 years or older.  All you need to do is modify the `handle` method to find those characters and emit their names to you.  

{% note %} 
This example only shows the handle method, but you still need all the rest of the code in the file too.
{% endnote %}

For example:

      def handle
        client.emit Character.all.select { |c| c.age >= 30 }.map { |c| "#{c.name} - #{c.age}" }
        client.emit_success "Done!"
      end

{% tip %} 
When doing a database query, make sure to do the 'map' at the end so you don't spam yourself with full database objects when all you really want is their name (or in this case, name + age).
{% endtip %}

You can also use the tinker command to update things in the database.  For example, if you wanted to change Bob's hair color (and didn't want to use the demographic/set command because that would be too easy):

      def handle
        char = Character.find_one_by_name("Bob")
        char.update_demographic("hair", "Gray" )
        client.emit_success "Done!"
      end

You can even combine the two - a query and an update - to act on a list of characters.  Say you changed a faction's name and wanted to update everyone with the old faction name to the new one:

      def handle
        chars = Character.all.select { |c| c.group("Faction") == "Old Faction" }
        chars.each do |c|
            Demographics.set_group(c, "Faction", "New Faction")
        end
        client.emit_success "Done!"
      end


## Multiple Tinkerers

Tinkering is set up with the assumption that only one person will be tinkering at a time, because frankly most games only have one coder.  In the remarkable event that you have multiple coders wanting to tinker at the same time, they'll just have to take turns or create their own personal tinker commands.