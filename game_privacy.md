---
title: Data and Privacy on Ares Games
layout: page
---

It's up to each individual Ares game to determine their privacy policies.  Ideally this will be conveyed to players in the terms of service acknowledgement or a policy file on the wiki.  This article provides some **general** information about privacy on Ares games.

{% include toc.html %}

## Overview

{% note %}
This article is about AresMUSH games.  For AresCentral and aresmush.com privacy practices, see the [aresmush.com website privacy policy](http://aresmush.com/privacy.html).
{% endnote %}

**Ares has no built-in commands to support admins spying on players.**  That means there's no SUSPECT flag or DARK power for spying, and no admin commands to view private scenes, mail, or private messages.  

Just as with any online service, though, **any** data transmitted to the server and/or stored in the database is ultimately accessible to the game owner and anyone they choose to share it with. Owners/coders may install custom loggers, create custom commands, or crack open the database manually. Sensitive information is best kept off-game.

## What Data Is Stored

It’s important to draw a distinction between **logged** and **stored** data.

*Debug logs* are plain-text, accessible by any admin to track and troubleshoot what happens on the game. **Certain commands are not logged for privacy reasons**: connect/create (due to passwords), mails, pages/pms, poses, oocs, channel chat, and others.

```
2023-01-30 17:31:36 INFO - Character Connected: Faraday 127.0.0.1 localhost 
2023-01-30 17:31:37 DEBUG - AresMUSH::Jobs::JobsFilterCmd: ID=1 Enactor=Faraday Cmd=job/filter mine 
2023-01-30 17:31:38 DEBUG - AresMUSH::Who::WhoCmd: ID=1 Enactor=Faraday Cmd=who 
```

*Stored data* (in the database) is for the purpose of game features. This enables things like the web portal play screen, channel recall, sharing scenes on the wiki, etc. **All built-in commands limit stored data to people who should have access to it.** Game admin do not have ready access to everything, not even headwiz. See "Who Can View Your Data" below for details.

Here are the types of personal data that can be stored by the game:

* The **IP Address** and hostname you're connecting from is saved every time you connect.
* Your **email address** and timezone is saved if you choose to provide it.
* Your Ares **player handle**, friends list and handle preferences are saved if you choose to link a character to your handle.
* **Conversations**--channel chat, private messages, poses and OOC chat (if a scene is started) and mail messages--are all saved to the database and may contain personal information. (i.e. if you're chatting with your buddy about your family/job/hometown/etc.)

## How Data Is Stored

Your data can be stored in either the game's database, or debug log files on the server.

Conversations and passwords are **only** stored in the database, never in debug logs.

Neither the database nor the log files are encrypted.  Passwords are hashed.


## Who Can View Your Data

All built-in commands limit stored data to people who should have access to it, as described below. But again we'll reiterate:

> Just as with any online service, **any** data transmitted to the server and/or stored in the database is ultimately accessible to the game owner and anyone they choose to share it with. Sensitive information is best kept off-game.

This section summarizes access to various kinds of game data.

### Channels

<table class="table">
  <tbody>
    <tr>
      <td class="privacy-col"><b>Who Can View</b></td>
      <td>
        Any player on the channel can view the chat history. New players may join the channel at any time and view past conversations.
      </td>
    </tr>
    <tr>
      <td><b>Reporting Issues</b></td>      
      <td>
        The chat report command/button can be used to report a channel conversation to the game admin in the case of harassment or abuse.
      </td>
    </tr>
    <tr>
      <td><b>How It's Deleted</b></td>
      <td>
        Channel chat cannot be deleted, though eventually old messages will be pushed out of the history buffer by new ones.
      </td>
    </tr> 
    <tr>
      <td><b>Admin Access</b></td>
      <td>Admins may join any channel and see the chat history.</td>
    </tr>       
  </tbody>
</table>

### Private Messages


<table class="table">
  <tbody>
    <tr>
      <td class="privacy-col"><b>Who Can View</b></td>
      <td>
        Any player involved in the conversation can view the message history. If someone is added mid-conversation, a new conversation is started (i.e. the new person will NOT see what came before).
      </td>
    </tr>
    <tr>
      <td><b>Reporting Issues</b></td>
      <td>
        The PM report command/button can be used to report a PM conversation in the case of harassment or abuse.
      </td>
    </tr>
    <tr>
      <td><b>How It's Deleted</b></td>      
      <td>
        Private messages time out on a game-configured interval, and are also deleted when a character idles out.
      </td>
    </tr>
    <tr>
      <td><b>Admin Access</b></td>
      <td>There is no built-in command allowing game admins to view other players' private message conversations.</td>
    </tr>           
  </tbody>
</table>

### Scenes


<table class="table">
  <tbody>
    <tr>
      <td class="privacy-col"><b>Who Can View</b></td>
      <td>
        <p>Open scenes are visible to everyone.  Private scenes are visible only to those who have been invited.  In both cases, scene logs include all poses and OOC chat.  </p>
        <p>
        Any scene participant may extend invitations, download the log, or share the log on the web portal when the scene is complete. In other words, don't assume a 'private' scene is going to _stay_ private.
       </p>   
      </td>
    </tr>
    <tr>
      <td><b>Reporting Issues</b></td>
      <td>
        The scene report command/utton can be used to report a PM conversation in the case of harassment or abuse.
      </td>
    </tr>
    <tr>
      <td><b>How It's Deleted</b></td>      
      <td>
        Unshared scenes may be deleted (either by request or on a game-configurable timer). There is a warning before this happens, to give participants the chance to download, restart, or share the scene.        
      </td>
    </tr> 
    <tr>
      <td><b>Admin Access</b></td>
      <td>There is no built-in command allowing game admins to view or join private scenes.</td>
    </tr>  
  </tbody>
</table>


### Mail

<table class="table">
  <tbody>
    <tr>
      <td class="privacy-col"><b>Who Can View</b></td>
      <td>
        Mail messages are visible to recipients, and may be forwarded to others.
       </p>   
      </td>
    </tr>
    <tr>
      <td><b>Reporting Issues</b></td>
      <td>
        The mail forwarding command can be used to report an abusive message.
      </td>
    </tr>
    <tr>
      <td><b>How It's Deleted</b></td>      
      <td>
        You can delete a mail you're received. Received mail is deleted when a character idles out.
      </td>
    </tr> 
    <tr>
      <td><b>Admin Access</b></td>
      <td>There is no built-in command allowing game admins to view other players' mail messages.</td>
    </tr>  
  </tbody>
</table>


### Other Data

Your player handle is visible to all players. There is no built-in command allowing admins to view your handle preferences, such as your friends list.

Email address, if set, is visible to game admins and can be cleared at will.

Your IP address is visible to game admins. This is NOT cleared on idled-out characters for security reasons.

The Ares web portal sets a cookie to remember you when you log back in. You can manage cookies through your browser.

## How to Delete Your Data

Most data can be manually deleted, or is automatically deleted on idle-out or a timer. See above for details.

If you want other personal information deleted, you will need to contact the game admins to request it.

## How Data Is Transmitted

This is not really Ares-specific, but it's good to be aware of: If you're using a MU client, your connection is extremely insecure. Data is transmitted from your PC to the game in plain text with no encryption, and could easily be intercepted.

Most Ares web portals will use HTTPS for security.  Those that don't are just as insecure as a MU client.