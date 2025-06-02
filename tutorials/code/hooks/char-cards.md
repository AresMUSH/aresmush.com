---
title: Custom Character Scene Cards
description: 
layout: page
tags:
- code
- custom hooks
---

> This [custom code hook](/tutorials/code/custom-hooks.html) is part of the Scenes plugin.

Character cards are mini-profiles that are shown when you click on a character's icon next to their pose.  There are two ways to customize the character cards:

1. Add a new tab to the system area with custom content.
2. Completely replace the card with your own design.

## Card Data

There are a number of character fields available for use in the template.  You use them like `this.char.name` or `this.char.description`.

| Field | Description |
|----|----|
| `name` | Character name. |
| `demographics` | A list of all demographics, each with `name` and `value` properties. |
| `groups` | A list of group affiliations and rank, each with `name` and `value` properties. |
| `all_fields` |  Contain group, demographic, and rank data in a form where you can easily look up specific values, like `char.all_fields.faction` or `char.all_fields.height`. |
| `description` | Current description. |
| `status_message` | Special status, like NPC. |
| `is_ooc` | If the character is an OOC bit, like a staffer or playerbit. |
| `icon` | Icon data. |
| `custom` | Any custom fields you define, as explained below. |

You can add data to the `this.char.custom` section by modifying the `custom_char_card_fields` method in `aresmush/plugins/scenes/custom_char_card.rb`

For example, if you wanted to show RP Hooks you could do:

    def self.custom_char_card_fields(char, viewer)
      {
         hooks: Website.format_markdown_for_html(char.rp_hooks)
      }
    end

You'll want to use the markdown formatter for freeform text that might include ansi or markdown codes.

Once you've made the data available, use it in your web template like so:

<pre>
    &#x7b;&#x7b;this.char.custom.hooks}}
</pre>

## Add New Tabs

If all you want to do is add new tabs to the card (e.g,. for your own custom skill system or plugin), you can just modify these two files:

- `ares-webportal/app/components/char-card-custom-tabs.hbs`
- `ares-webportal/app/components/char-card-custom-tabs-content.hbs`

The 'tabs' file defines the tab, and the 'tabs-content' file contains its content. You can define multiple tabs and multiple panes of tab contents in these files.

## Replace the Card Template

To replace the character card entirely, set `use_custom_char_cards` to `true` in the [scenes configuration](/tutorials/config/scenes.html)

Initially, your custom card will be blank.  To make it show something, you'll need to put some code into  `ares-webportal/app/components/char-card-custom.hbs`.

You'll probably want to start by copying the code from the [standard template](https://github.com/AresMUSH/ares-webportal/blob/master/app/components/char-card.hbs) and pasting it into your custom card file.  You can then tweak it, add new styling, or completely change the look and feel.
