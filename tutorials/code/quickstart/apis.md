---
title: Common APIs
description: 
layout: tutorial
quickstartTutorial: true
tutorialName: Code Quickstart
tutorialIndex: tutorials/code/quickstart
prevstep: db-intro
nextstep: ruby-cmd
tags:
- code
- code-quickstart
- api
---

An API (Application Program Interface) is a well-defined way for one piece of code to talk to another piece of code.  Ares plugins provide APIs that let other plugins interact with them, and you can use these APIs in your own code.

Plugin APIs are always found in the file `plugins/<plugin>/public/<plugin>_api.rb`.  If you look in that file, you'll see what API methods that plugin provides. For example, in the `jobs_api.rb` file, you'll find API methods for:
  
    Jobs.create_job(category, title, description, author)
    Jobs.close_job(enactor, job, message)
    etc.

You'll find these APIs used throughout the Ares codebase.  The channel plugin creates a job when someone reports channel abuse.  The idle plugin creates a job when it's time to do the idle purge.  The chargen plugin creates a job when someone submits their app.  And so on.

{% tip %} 
APIs generally expect that permissions will be checked by the calling command handler.
{% endtip %}

## Try It!

Let's use the jobs API to create a test job. Change the tinker handle method as shown below:

    def handle
      Jobs.create_job("REQ", "A Test Job", "This is a test job.", enactor)
    end

## Common APIs

Here are a few other common APIs you may use in your own code.

### Create a Job

    Jobs.create_job(category, title, description, author)

You can use `Jobs.request_category` for the category to make it a request and `Game.master.system_character` to make the author "System" instead of a specific character.

### Send Mail

    Mail.send_mail(names, subject, body, client, author)

Use an array for `names` even if there's only one name, e.g. `[ "Faraday" ]`.
You can use `Game.master.system_character` to make the author "System" instead of a specific character.
Leave 'client' nil when sending automated messages.

### Move a Character

    Rooms.move_to(client, char, room, exit_name)

You can leave `client` nil if the character isn't logged in.
You can leave `exit_name` nil if they aren't moving through an exit.

### Emitting Based on Character

Emits go to *clients*, not characters, but sometimes you need to find the client associated with a character.  For example, if Harvey attacks Bob, you'll want to send an emit to Bob's client.  These login APIs help you do that.

    Login.find_client(char)
    Login.emit_if_logged_in(char, message)
    Login.emit_ooc_if_logged_in(char, message)

### Post to the Forum

    Forum.system_post(category, subject, message)

This creates a post from "System".

### Adding to Scenes

If you have a system that impacts RP (like magic or combat), you might want messages from that system to show up in RP logs.  Note that this method does *not* notify anyone in the game, so you'll also want to emit the message to the relevant people.

    Scenes.add_to_scene(scene, pose, character, is_setpose, is_ooc)

