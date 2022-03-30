---
title: Notifications
description: 
layout: page
tags:
- code
- engine
---

Although [basic emits](/tutorials/code/emitting.html) are great for command output, **notifications** are more broadly used to alert players to things happening in the game.

{% include toc.html %}


## What is a Notification?

There are many different kinds of notifications, which each serve a different purpose.

### Emits

Emits are specific notifications to players on a MU client.  They are not sent to the web portal.

{% include pretty_image.html file='notif-emit.png' %}

### Personal Notifications

Personal notifications are persistent alerts targeted to individual characters.  They're saved to the database, so folks won't miss anything.  You can view personal notifications by clicking the 'bell' icon on the web portal or using the `notices` command in-game.  

These notifications are associated with a specific kind of object - a mail message or a scene, for example.  They are marked as 'read' when you view the mail/scene/forum/etc. that it's notifying you about.

{% include pretty_image.html file='notif-login.png' %}

### Browser Notifications

Browser alerts are transient messages that appear in the bottom-right corner of the web portal.  Depending on the player's browser and computer settings, they may also appear in the computer's notification center.

{% include pretty_image.html file='notif-browser.png' %}

{% include pretty_image.html file='notif-pc.png' max-width="400px" %}


For a player to see these notifications in their computer's notification center:

<ul>
  <li>The browser must support notifications.</li>
<li>The player must click 'Accept' or 'Allow' when the game asks them if they want to allow notifications from the game's website. This can be changed later in the browser settings.</li>
<li>The game must be set up with HTTPS security.</li>
</ul>

### Game Channel

Low-priority messages are sent to the game announcements channel rather than directly to players. This allows players to mute/leave the channel when they don't want to be bothered.  This channel is named "Game" by default, though individual games can configure which channel is used.

{% include pretty_image.html file='notif-game.png' max-width="400px" %}

### Web Data Updates

Finally, you can send raw data to the web portal to update a page. For example, if someone poses in a scene, the game updates the scene live with the new pose data.  

Web data updates are not visible to the player, but rather contain raw data that is parsed and handled by the web portal.

## Notification Utilities

There are several notification utilities available in the code.

{% tip %}
Many events will trigger multiple notification mechanisms. For example, new scene activity will emit to the room, _and_ issue a personal notification to players who are offline _and_ use a web data notification to update live scene screens.
{% endtip %}

### Emits

Emits are sent to a specific player. If you're in a command handler, you might already have a client or room reference:

    client.emit message
    enactor.room.emit message

Otherwise you can find a character by name and then notify them with this utility:

    Login.emit_if_logged_in(char, message)

{% tip %}
Remember - emits aren't sent to the web portal, so you will often need to pair them with another type of notification.
{% endtip %}

### Emit + Browser Notification

Commonly you'll want to notify BOTH characters on the web portal and those on a MU client. The global notifier class can help.

{% include pretty_image.html file='notifications.png' %}

To notify all characters, you would do:

        Global.notifier.notify_ooc(:shutdown, message) do |char|
          true
        end

{% tip %}
The type (e.g., `:shutdown`), is just a symbol identifying the notification. This allows the web portal to act differently for different types of notifications. Here it's not important because the notification is just a raw message, so the web portal's default handling will suffice.
{% endtip %} 

You can put conditions into the block to limit the notification to only certain characters. Here the notification is limited to those characters who can read a forum category:

      Global.notifier.notify_ooc(type, message) do |char|
        char & Forum.can_read_category?(char, category)
      end

{% tip %}
The 'char' variable there can be nil for a connection who isn't logged into a character, so check it for nil before using it.
{% endtip %} 

## Personal Notifications

You can create a personal notification (aka login notice) for a character using this utility:

    Login.notify(recipient, :mail, message, message.id)

The type (`:mail`) and the reference ID (`message.id`) help the portal direct the player to the proper page to read the item.

{% tip %}
You can specify your own types instead of `:mail`.  However, if you want the web portal to show the 'View' button and let you navigate to a specific page, you'll need to modify `notifications.hbs` to add the navigation code.
{% endtip %} 

Ideally, you will mark notifications as read when they're no longer relevant. For example, you'd mark the mail notification as read once they've read the mail message. 

    Login.mark_notices_read(message.character, :mail, message.id)

Use the same type (`:mail`) and reference ID (`message.id`) that you used when creating the notification.

## Web Data Notification

Web data notifications are used to update info on the web portal _without_ emitting to the game, like adding a pose to a scene or a chat message to a channel.

{% note %}
Adding new web data notifications will require changes to the web portal code to properly handle them and do the necessary updates. This is probably the most complex code in the entire system, so it's not for the faint of heart.  If you're adventurous enough to give it a try, look for `new_combat_activity` in both the plugin and portal code for an example you can follow.
{% endnote %}

As with the global notifier, we can limit the notification to only certain characters.  Here we're only sending it to characters on a channel:

      web_message = "#{channel.name.downcase}|#{channel.name}|#{Website.format_markdown_for_html(formatted_msg)}"
      Global.client_monitor.notify_web_clients(:new_chat, web_message) do |char|
        char && Channels.is_on_channel?(char, channel)
      end

Notice that we're sending a bunch of data here (separated by pipe delimiters). Web client notifications contain data and not just a simple message for display.  The type (`:new_chat`) tells the web portal how to interpret the data.

## Game Channel

General game events are sent to the Game channel by default (though you can configure which channel). This includes miscellaneous updates like the who record being broken, and event starting, and so on.  Using a channel versus a global emit lets people mute these notifications when they're RPing and catch up on them later.

    Channels.announce_notification(message)
