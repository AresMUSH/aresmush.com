---
title: Using the Database
description: 
layout: page
tags:
- code
- database
---

Most commands will need to read data from or save data to the database.  Ares uses an off-the-shelf database tool called Redis.  The [Ohm](http://ohm.keyvalue.org/) database library lets you interact with the database directly from Ruby code.

{% include toc.html %}

## Models and Fields

Ohm lets you define ruby classes that interact with the database.  These are called **Models**, and you can identify them by the fact that they inherit from `Ohm::Model`.  Model classes define attributes that correspond to fields in the database.  For example, the `Character` class defines a name and alias: 

    class Character < Ohm::Model
      attribute :name
      attribute :alias
      ...
    end

You've probably seen database fields used throughout the code, in examples like `client.emit "Hello #{enactor.name}!"`   In that case, `enactor` is a character model, and `name` is the database field.

You'll need to look in the code to find out what database fields are available.

## Model Modules

All database models should live in the base AresMUSH module, not in individual plugins.

**CORRECT**

    module AresMUSH
      class MyThing < Ohm::Model
      end
    end

**INCORRECT**

    module AresMUSH
      module SomePlugin
        class MyThing < Ohm::Model
        end
      end
    end


## Queries

The [Ohm](http://ohm.keyvalue.org/) database library provides a variety of ways to query for database models, but here are a few of the easiest:

* `Character[id]` - Finds an object directly by ID.
* `Character.find_one_by_name(name)` - Finds the first character with that name/alias.
* `Character.find_any_by_name(name)` - Finds *all* characters with that name/alias.
* `Character.all` - Finds *all* characters.

If your database isn't gigantic, you can also use the Ruby `select` statement to filter objects based on any set of criteria.  If your database is huge, you're better off using [Ohm's](http://ohm.keyvalue.org/) queries.  They're a little more complex, but faster.  Here's an example that will find all characters with the 'admin' role:


    def handle
      chars = Character.all.select { |c| c.has_any_role?("admin") }
      names = chars.map { |c| c.name }
      client.emit "You found #{names.join(", ")}"
    end

{% tip %} 
It is common to use  `select`  and  `map`  together like this.  Select will find a bunch of database objects, and map will get just the field you need from them (in this case the name).
{% endtip %}

### Game Model

The Game model is special because there's only one game. You don't really need to search for it. You can access the one and only game model using:

    Game.master

## Accessing Fields

Once you have a database object, you can use its properties as simple methods.  For example:

    char = Character.find_one_by_name("Bob")
    client.emit "Hello #{char.name}!"

## Updating Fields

You can update the properties on a database object using the `update` method.  For example:

    char = Character.find_one_by_name("Bob")
    char.update(name: "Harry")

Many database properties have specialized update methods because their data storage is not so straightforward.  Look around for helper methods in the plugin module:

    char = Character.find_one_by_name("Bob")
    Demographics.set_group(char, "Faction", "Navy")

{% note %} 
Do not attempt to change database properties just by updating the object (e.g. `char.name = "Harry"`)  This changes the property on the <b>object</b> but does not actually update the database.  You can legitimately use this method to change multiple properties as a batch, but you have to do `char.save` at the end to commit the changes to the database.
{% endnote %}

## Field Types

Under the hood, all redis fields are stored as strings. The Ohm database library provides some utilities to let you tell the Ruby code to _interpret_ certain fields as different data types, as shown below:

    attribute :team, :type => DataType::Integer
    attribute :freshly_damaged, :type => DataType::Boolean
    attribute :armor_specials, :type => DataType::Array, :default => []
    attribute :prior_ammo, :type => DataType::Hash, :default => {}
    attribute :starts, :type => DataType::Time
    attribute :birthdate, :type => DataType::Date    

{% note %}
You may want to define default values for fields using other data types, especially hashes and arrays (which would otherwise be nil).
{% endnote %}

## Finder Helpers

There are a few convenient utilities to help with common searches.  All of these will search by name or (for players) by alias, and include the `me` or `here` keywords, so they require you to pass in the character doing the search.

* `ClassTargetFinder` - Searches for a single object of the specified type.
* `AnyTargetFinder` - Searches for a single object among rooms, characters or exits.  Helpful for commands like describe/destroy that can work on multiple object types.
* `OnlineCharFinder` - Searches for a single matching online character.
* `VisibleTargetFinder` - Searches for a matching object in the same room - either a character, room or exit.  

All of the finder helpers do the error handling necessary to translate multiple matches into a message like "I don't know which one you mean" and no matches into "I don't see that here".  They return a `FindResult` object containing a 'found' indication and **either** the target object **or** an error message.

    result = ClassTargetFinder.find(name, Character, searcher)
    if (result.found?)
        # Object was found - do something with result.target
    else
       # Object was not found - do something with result.error
    end

## Target Finder Block helpers

Several of the more commonly-used target finders have another level of helper utility you can use.  Here's how it works:

    ClassTargetFinder.with_a_character(name, client) do |model|
        # Do something with model if it's found
    end

`with_a_character` will do the stuff in-between the `do` and the `end` if the character was found, using the variable `model` for the character it found. If the character was not found, it will emit the appropriate error message to the client.

There's a similar helpers for `with_something_visible` and `with_online_chars`.

{% tip %}
These versions are generally superior to the basic helpers because they take care of the error messages for you.
{% endtip %}

## Callback Methods

Some database models use **Callbacks** - methods that are triggered in response to certain database events.  There are two possible callbacks in Ares, called before an object is deleted or before it's saved:

* `before_delete` -  If an object has any references, you may want to delete them before the object itself is deleted.  For example, a room might delete all of its exits when it's getting deleted.
* `before_save` - If an object has special fields, you may set them before the object is saved.  For example, if you store the uppercase version of the object name for fast lookups, you want to update that to match the object name every time the object is saved.

## Relationships - References, Sets and Collections

Although Redis is not a relational database like SQL, we still need to define _relationships_ between our objects. A mail message has an author and recipients (all characters), a scene is attached to a room, etc.  Ohm provides some built in concepts that let us manage these relationships.  See [Database Relationships](/tutorials/code/db-relationships.html).
