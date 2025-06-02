---
title: Custom Character Fields
description: 
layout: page
tags:
- code
- custom hooks
---

> This [custom code hook](/tutorials/code/custom-hooks.html) is part of the Profile and Chargen plugins.

With custom code, you can add new fields to the character profile and/or chargen.  There is an entire step-by-step tutorial for doing this, using [Character Goals](/tutorials/code/add-web) as an example.  Below is a quick reference to the files you'll need to modify.

{% tip %}
You can mix and match the three sections: Profile Display, Profile Editing, Chargen.  Maybe you have a field that's set by staff using an in-game command, and you just want to show it but not let anyone edit it.  Maybe you have a secret field that you want players to set in chargen but not show anywhere.
{% endtip %}

## Profile Display

You can add a new tab for your custom data to the "System" section of the profile.

* Define the tab navigation control: `ares-webportal/app/components/profile-custom-tabs.hbs`
* Define the tab contents: `ares-webportal/app/components/profile-custom.hbs`
* Add any buttons or actions, if needed: `ares-webportal/app/components/profile-custom-tabs.js`
* Add the code to return data to the web: `aresmush/plugins/profile/custom_char_fields.rb` (`get_fields_for_viewing`)

## Profile Editing

You can add a new tab with controls to edit your custom data in the profile edit screen.

* Define the tab navigation control: `ares-webportal/app/components/char-edit-custom-tabs.hbs`
* Define the tab contents: `ares-webportal/app/components/char-edit-custom.hbs`
* Add any buttons or actions, as well as packaging the new data to send to the game: `ares-webportal/app/components/char-edit-custom.js`
* Add the code to return data to the web and save the data from the web: `aresmush/plugins/profile/custom_char_fields.rb` (`get_fields_for_editing` and `save_fields_from_profile_edit2`)

## Chargen

You can add a new tab to chargen with controls to set your custom data.

* Define the tab navigation control: `ares-webportal/app/components/chargen-custom-tabs.hbs`
* Define the tab contents: `ares-webportal/app/components/chargen-custom.hbs`
* Add any buttons or actions, as well as packaging the new data to send to the game: `ares-webportal/app/components/chargen-custom.js`
* Add the code to return data to the web and save the data from the web: `aresmush/plugins/profile/custom_char_fields.rb` (`get_fields_for_chargen` and `save_fields_from_chargen`)
