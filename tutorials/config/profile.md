---
title: Configuring the Profile System
layout: page
tags:
- config
---

To configure the Profile plugin:

1. Select Admin -> Setup.
2. Edit `profile.yml`

{% include toc.html %}

## profile_title_format

The title bar on character pages can show different versions of the name, determined by this config option.

* bitname - Just the regular character bit name.
* military - Rank, callsign, and first/last name (pulled from fullname), e.g., Captain William "Husker" Adama.
* fullname - The 'fullname' demographic.
* nickname - If your game uses nicknames, this will use the name + nickname using whatever format you've specified, e.g., Steve ("Captain America").

## backup_commands

You can customize what commands get executed when someone does the `backup` command.  By default it will include their profile, description, sheet and damage.

## Custom Character Fields

With custom code, you can add new fields to the character profile and/or chargen.  See [Custom Character Fields](/tutorials/code/hooks/char-fields.html).