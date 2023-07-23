---
title: Configuring the Idle System
layout: page
tags:
- config
---

To configure the Idle plugin:

1. Select Admin -> Setup.
2. Edit `idle.yml`

{% include toc.html %}

## use_roster

You can turn the roster system on or off by setting `use_roster` to true or false. Note: You'll probably also want to edit the [web navbar]({{site.baseurl}}/tutorials/config/website.html#changing-the-navbar) to remove the Roster menu item.

## days_before_idle

You can configure how long someone has to be idle (e.g. not logged in) before they appear on the idle sweep.

## idle_warn_msg

The mail message sent to someone when they are given an idle warning.

## idle_exempt_roles

Since special characters may not log in often, you can exempt certain roles from the idle sweep.  There are two ways to do this.  The first way is to list a number of roles.  For example, this would make everyone with the builder, admin or guest role exempt from the idle sweep:

    - admin
    - builder
    - guest

If you want more fine-tuned control - e.g. only exempting certain admins and not all of them, you could create a special `idle_exempt` role and assign it only to specific people who are exempt from the idle policy.

## idle_category

When characters are idled out, an annnouncement is posted to the forum.  You can configure which category they go to.  Making it a forum that doesn't exist will effectively disable the welcome post.

## Idle Sweep Reminder

Since idle sweeps must be done manually, the idle system will periodically create a staff job to remind you to do it.  There are several settings related to this reminder:

`monthly_reminder_cron` - This cron job controls when the reminder happens.  By default it's monthly.  See the [Cron Job Tutorial](http://www.aresmush.com/tutorials/code/cron.html) for help if you want to change this.

`monthly_reminder_title` - The reminder's job title.

`monthly_reminder` - Text for the reminder job.

`reminder_category` - The job category that the reminder will be put into.

## Roster Announcement

When characters are taken off the roster, an arrival announcement is also posted to the forum.  

### arrivals_category

You can configure which category this goes to by setting `arrivals_category`.  As with the Idle announcement, you can make it a non-existent forum to disable the post.

### roster_arrival_msg

You can configure the contents of the arrival announcement.  You can use `%{name}` in the message where you want the char's name to go.  You can also use `%{rp_hooks}` for their RP Hooks, or any group name.  For example:  `"Welcome %{name} - the newest %{position} in %{faction}.\n\nRP Hooks:\n%{rp_hooks}"`  (The quotes there are important.)

{% tip %}
Make sure the groups used in the message actually exist, or you'll get an error when you try to approve someone. 
{% endtip %}

### roster_welcome_msg

This message is mailed to a new player when they are taken off the roster.  You might use this to tell them any special instructions for getting started.

## restrict_roster

Set this to true if you want **all** characters on the roster to require an application.

## default_contact

If a character on the roster doesn't have a specific contact person (for questions about the character), this will used.  It defaults to "Admin" but you could make it a specific person or something like "App Staff".

## roster_fields

You can configure which fields appear on the roster list.  For each field, you can specify the column title, width, and where to get the data.  For example, this config makes two columns (25 wide and 15 wide) showing name and position.

    - field: name
      width: 25
      title: Name
    - field: group
      value: position
      width: 15
      title: Position

A complete description of all available fields - and how to create custom fields - can be found in the "who_fields" option in the [Who/Where Configuration](/tutorials/config/who.html).

## roster_app_template

You can use this field to tell players what information is required for a roster application.

## roster_app_category

Roster applications will use this job category.