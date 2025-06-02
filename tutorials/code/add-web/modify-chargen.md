---
title: Modifying Chargen
description: 
layout: tutorial
prevstep: edit-request
nextstep: next-steps
tutorialIndex: tutorials/code/add-web
addWebTutorial: true
tutorialName: Modifying the Web Portal
tags:
- code
- website
---

We addressed editing goals from the character profile page, but what about during character creation?  That actually will require us to modify another set of templates and handlers.  Here's a starting point - see if you can figure out how to add goals to chargen:

- Chargen custom code hooks: `aresmush/plugins/profile/custom_char_fields.rb` (`get_fields_for_chargen` and `save_fields_from_chargen`)
- Chargen template: `ares-webportal/app/components/chargen-custom-tabs.hbs` and `ares-webportal/app/components/chargen-custom.hbs`
- Chargen controller: `ares-webportal/app/components/chargen-custom.js`

{% note %}
save_fields_from_chargen allows you to return error/warning messages.  Always return a list from that method--either `return []` if everything's OK, or a *list* of messages like `return [ "Something was bad." ]` or `return [ "Something was bad.", "Something else was also bad." ]`.
{% endnote %}

Don't forget, you can always [ask for help](/feedback.html) if you get stuck.