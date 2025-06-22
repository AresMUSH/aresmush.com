---
title: Database Queries and Updates
description: 
layout: tutorial
quickstartTutorial: true
tutorialName: Code Quickstart
tutorialIndex: tutorials/code/quickstart
prevstep: localization-intro
nextstep: apis
tags:
- code
- code-quickstart
- database
---

Most commands will need to read data from or save data to the database.  Ares uses an off-the-shelf database server called Redis, but you won't interact with the database directly.  There are no SQL queries to write or anything like that.  The [Ohm](http://ohm.keyvalue.org/) database library lets you interact with the database using Ruby code.

Diving deep into the database is beyond the Quickstart Tutorial.  This is just a quick overview, and we'll cover more in the later tutorials.  There's also a separate  [database tutorial](/tutorials/code/database.html) for you in the Advanced Coding section when you get more comfortable.

## Models and Fields

Ohm lets you define ruby classes that interact with the database.  These are called **Models**, and you can identify them by the fact that they inherit from `Ohm::Model`.  Model classes define attributes that correspond to fields in the database.  For example, the `Character` class defines a name and alias: 

    class Character < Ohm::Model
      attribute :name
      attribute :alias
      ...
    end

We're already seen how we can utilize the name attribute in our code through examples like `client.emit "Hello #{enactor.name}!"`   In that case, `enactor` is an instance of a character model, and `name` is the database field.

## Try It! - Queries

There are a variety of ways to query (request) information from the database, but the most common one will be to find something by name.  Let's see how that works.  Change the tinker command as shown:

    def handle
      char = Character.all.select { |c| c.name == cmd.args }.first
      if (char)
        client.emit "You found #{char.name}"
      else
        client.emit "Nothing found."
      end
    end

Try the command with different names and see what happens.

You may have noticed that this version will not find "Faraday" if you typed "faraday" - it's very literal.  It also won't search by alias.

Since searching by name is so common, there's a utility method to help you with these things.  Change the `char = ` line in the handle method to this:

    char = Character.named(cmd.args)

Now try the searches again with aliases and different capitalization.  It works much better.

There are some other query helpers, which you can read about in the advanced [database tutorial](/tutorials/code/database.html) when you're ready.

## Try It! - Updates

Once you have the database object, you can use the `update` method to change its fields.  Here's how we can change the System character's alias:

    def handle
      char = Character.named('System')
      char.update(alias: "sys")
      client.emit "Done!"
    end

{% note %} 
Just setting the class attribute (like `char.alias = 'guest'`) will change the local copy of the object, but it doesn't update the database.  Always call `update` to make database changes.
{% endnote %}

