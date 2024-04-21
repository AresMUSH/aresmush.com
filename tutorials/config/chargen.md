---
title: Configuring the Chargen System
tags:
- config
layout: page
---

To configure the Chargen plugin:

1. Select Admin -> Setup.
2. Edit `chargen.yml`

{% include toc.html %}

## Messages

You can configure the messages that are put into the approval job when characters are approved or rejected.  Commonly you will edit the approval message to tell new players anything special they need to know to get started.

### approval_message and rejection_message

These messages are added to the approval job in response to the approve/reject commands.

### post_approval_message

The system will create a new admin-only job *after* someone is approved. This job will remind the game admin to do any ancillary tasks, like adding the new character to lists, or making sure they have a log icon or a home.  You can configure the list of reminders.

{% tip %}
Leave the message blank to disable creation of the post-approval job.
{% endtip %}

### welcome_message and arrivals_category

The system will post a welcome message to the forum (in `arrivals_category`) to announce approval of a character.

{% tip %}
The welcome post will not be created for NPCs or characters who are added to the roster before they're approved. Leave the arrival category blank to disable the creation of the welcome post entirely.
{% endtip %}

You can use `%{name}` in the message where you want the char's name to go.  You can also use `%{nick}` for the formatted name/nickname, `%{rp_hooks}` for their RP Hooks, or any group name.  For example:  `"Welcome %{name} - the newest %{position} in %{faction}.\n\nRP Hooks:\n%{rp_hooks}"`  (The quotes there are important.)

{% note %}
Make sure the groups used in the welcome message actually exist, or you'll get an error when you try to approve someone. 
{% endnote %}

## Web Chargen Blurbs

You can also configure the character creation instructions that appear in the Web Chargen.

* `bg_blurb` - Background instructions.
* `hooks_blurb` - RP Hook instructions.
* `desc_blurb` - Description instructions.
* `groups_blurb` - Group instructions.
* `demographics_blurb` - Demographics instructions.
* `rank_blurb` - Description of the rank field.
* `icon_blurb` - Instructions for uploading a profile icon.

{% tip %} 
Abilities instructions are set up in the [FS3Skills Chargen Config](/tutorials/config/fs3skills_chargen.html).
{% endtip %}

## allow_web_submit

This setting controls whether characters can submit their application from the web portal.  If your game isn't using FS3 and doesn't have the ability to set stats via the web, you'll probably want to disable this to force people to complete chargen in-game.

## app_review_commands

You can configure which commands execute when you do `app/review`.  Just supply a list of commands, and use %{name} where you want the character's name to go in the command.  For example:

    - app %{name}
    - profile %{name}
    - bg %{name}

## Application  Jobs

You can edit the categories and states that the chargen system uses for its application jobs.

* `app_category` - Character applications use this category.
* `app_resubmit_status` - When an app is re-submitted, the job enters this state.
* `app_hold_status` - When an app is rejected, the job enters this state.

## hooks_required

You can configure whether RP hooks must be set in chargen or not.

## max_bg_length

Used to specify a maximum length of a background, in characters. Set it to 0 to allow bgs of unlimited length. Note: This is not a hard stop, but shows up in app review during chargen.

## stages

Character creation is done as a series of 'stages'.  For each stage, you can choose to display either a help file, a title and text, or both.

For example, the following config will show custom text for the first stage, a help file for the second, and both text and a help file for the third.

    start:
        title: "A Title"
        text: "Some text about starting chargen."
    sheet:
        help: 'sheet'
    demographics:
        help: 'demographics'
        text: 'Some extra help text you want to say about demographics.'

{% tip %} 
Make sure the help file actually exists. It should exactly match the help file name (without the .md extension).
{% endtip %}

## Custom App Review

With custom code, you can add extra automated system checks on the App Review screen in chargen, like making sure their groups make sense.  See [Custom Chargen App Review](/tutorials/code/hooks/app-review.html).

## Custom Approval Triggers

With custom code, you can automate certain actions to be taken when a character is approved, like adding people to channels or roles.  See [Custom Chargen Approval Triggers](/tutorials/code/hooks/approval-triggers.html).

## Custom Character Fields

With custom code, you can add new fields to the character profile and/or chargen.  See [Custom Character Fields](/tutorials/code/hooks/char-fields.html).

## Public Backgrounds

Backgrounds are private by default. Characters may copy their BG (or an abridged version) into a character profile field if they wish.

If you want backgrounds to be visible to everyone automatically, just give everyone the `view_bgs` permission. See [Roles and Permissions](/tutorials/manage/roles.html) for details.

