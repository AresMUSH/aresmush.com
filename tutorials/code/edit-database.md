---
title: Edit Database Fields
description: 
layout: page
tags:
- code
- database
---

On Penn and Tiny, you can change settings just by manually editing attributes:

    &WHATEVER *Player=Something

That doesn't work on Ares because objects and attributes work differently.

# Admin Commands

The "Ares Way" is to use admin commands for these sorts of things.  Need to edit someone's skills?  Use the `ability` command.  Need to edit someone's actor?  Use the admin `actor` commands.

> See `help` for a complete list of admin commands.

# Tinkering

Sometimes there won't be an admin command for what you need.  In those cases you can use the `tinker` command.  See the [Tinkering](/code/tinker.html) tutorial.

# Manual Database Access

It's rare when you can't do what you need with tinkering.  After all - tinkering can do everything the code can do.  

But if you ever get into that situation, it's time to roll up your sleeves and dive into the database itself.  Log into your [Server Shell](/tutorials/manage/server-shell.html) and run the following commands to open up a database command prompt:

    redis-cli
    auth YOUR_DATABASE_PASSWORD

From here you can use any [redis commands](http://redis.io/commands).

For example, to see a list of all character objects:

    keys *Character* 

This will give you a list of items like `AresMUSH::Character:2`.

These objects are hashes, so you use the redis HGET/HST commands to access them.  For instance, to view someone's pose autospace field setting:

    hget AresMUSH::Character:2 pose_autospace

You can look in the code to find the field names (like pose_autospace), or you can just ask for all of them at once.

    hgetall AresMUSH::Character:2

Also keep in mind that many settings are stored in a child object and referenced by ID.  For instance, to find out the name of the room someone's in:

    hget AresMUSH::Character:2 room_id  --> gives '1'
    hget AresMUSH::Room:1 name --> gives 'Welcome Room'

You can change things with the `hset` command:

    hset AresMUSH::Character:9 pose_quote_color "%xr"

{% note %} 
Be careful when changing fields manually.  Formatting matters, and because you're bypassing the game's internal error-checking you might set a field to an invalid value.  For example, setting a character's room ID to a room that doesn't exist would cause an error when the character logged in.
{% endnote %}


