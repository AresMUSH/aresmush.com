---
title: Configuring the Login System
layout: page
tags:
- config
---

There are several things you can configure about character logins.

{% include toc.html %}

## Connect Screen

To configure the Connect Screen:

1. Go to the Web Portal's Admin screen.  
2. Select 'Connect Screen'.

The connect screen can contain all the usual MUSH formatting codes (including color!), but you don't need to put in %r for linebreaks or %b for spaces.  The game will respect what's in the file as it appears.

## Terms of Service

By default, the game will present a Terms of Service file to new users.  You can disable this by setting `use_terms_of_service`, as explained below.

{% tip %} 
If your TOS is long, it's recommended that you just link to a wiki/web page rather than spamming new players with a giant wall of text.
{% endtip %}

To configure the Terms of Service:

1. Go to the Web Portal's Admin screen.  
2. Select 'Terms of Service'.

The TOS can contain all the usual MUSH formatting codes, but you don't need to put in %r for linebreaks.  The game will respect what's in the file.

{% tip %} 
If you ever make important changes to the terms of service, you probably want to force existing characters to read them again.  To do this, use the  `tos/reset`  command in-game.  Everyone will be forced to acknowledge the new terms of service the next time they log in.
{% endtip %}

## Allowing Logins

There are several ways to configure who can create characters and connect. For each setting, there is a corresponding message option that lets you provide an optional reason why it's not allowed. For example: "Logins are disabled at this time. YOUR REASON GOES HERE"

1. Select Admin -> Setup.
2. Edit `login.yml`


| Config Option | Purpose | Reason Option |
| `allow_web_registration` | Whether players can use the Register page to create a new character from the web portal. | `registration_not_allowed_message` |
| `allow_game_registration` | Whether players can use the `create` command to make a new character from a MU client. | `registration_not_allowed_message` |
| `disable_nonadmin_logins` | Set this true if you need to shut down connections to everyone except game admins. | `login_not_allowed_message` | 
| `portal_requires_registration` | Requires a login for everything on the portal, even normally public things like the wiki and scene logs. | n/a |

If you want more fine-grained control, you can use the [Roles System](/tutorials/manage/roles.html) to control which roles have the 'login' permission.  By default, this permission is assigned to the 'everyone' role, meaning all characters can log in.  During development, you may want to remove it from everyone and add it only to ancillary staff like builders or wiki developers. 

<a name="guests"></a>

## Configuring Tours (Guests)

Ares no longer supports pre-made shared guest characters. Instead, the `tour` command (aliased to `connect guest`) and web portal Tour button let players create a temporary character with an auto-generated name and password. Other than the way their name/password is set, these characters are identical to new characters created from the Register screen/`create` command. They can be made into permanent characters just by changing their name/password.

### Guest Names

You can configure what names are used for temporary characters.

1. Select Admin -> Setup.
2. Edit `names.yml`
3. Edit the `guests` list.

{% note %}
Temporary characters are recycled with the idle purge just like any other new character. If all the guest names are in use, the system will just use a name like `Guest-1` with an incrementing number. To avoid this, just make sure you have enough names on the list to cover you between idle purges. You can also run an idle purge at any time.
{% endnote %}

### Enabling Tours

You can configure where guests are allowed and customize the message shown if they're disabled.

1. Select Admin -> Setup.
2. Edit `login.yml`

| Config Option | Purpose | Reason Option |
| `allow_web_tour` | Whether players can use the Tour feature from the web portal. | `tour_not_allowed_message` |
| `allow_game_tour` | Whether players can use the Tour feature from the `tour` or `connect guest` commands. | `tour_not_allowed_message` |

### tour_welcome_message

This message is sent via mail when someone creates a temporary guest character and will include the `%{name}` and `%{password}` variables to tell them their temporary name and password.

## Other Configuration

To configure the rest of the Login plugin:

1. Select Admin -> Setup.
2. Edit `login.yml`

### use_terms_of_service

You can disable the terms of service completely by setting `use_terms_of_service` to false.

### activity_cron

This cron job controls when the login activity tracker is updated.  By default it's hourly.  You shouldn't change this.

### blacklist_cron

This cron job controls how often the site blacklist is updated.  By default it's bi-monthly.  You shouldn't need to change this.

### notice_cleanup_cron and notice_timeout_days

This cron job controls how often the old notifications are cleared out.  By default it's monthly.  You shouldn't need to change this. You can also configure how long old notifications are kept before they're deleted.

### boot_timeout_seconds

Controls how long someone is in timeout after being booted. This is meant as a short deterrent to discourage trolls, and is not meant as a long-term penalty. Remember that in the default configuration, all approved players are allowed to boot (to protect each other from disruptive guests/newbies), so you probably don't want to make it more than a few minutes.