---
title: Modifying the Edit Template
description: 
layout: tutorial
nextstep: edit-request
prevstep: get-template
tutorialIndex: tutorials/code/add-web
addWebTutorial: true
tutorialName: Modifying the Web Portal
tags:
- code
- website
---

Finally, we modify the web portal to let us enter some goals. A custom code hook lets us add new tabs to the character edit screen without touching the core code.

## Define the Tab Navigation

First we're going to define the tab navigation control.  Edit `ares-webportal/app/templates/components/char-edit-custom-tabs.hbs` and add:

        <li><a data-bs-toggle="tab" class="nav-link" href="#goals">Goals</a></li>

## Define the Tab Contents

Next we'll define the contents of the tab.  This lives in a _different file_, so edit `ares-webportal/app/templates/components/char-edit-custom.hbs` and add:

<pre>
        &lt;div id="goals" class="tab-pane fade in">
          &#x7b;&#x7b;markdown-editor text=this.char.custom.goals}}
        &lt;/div>
</pre>

{% tip %}
The name in `id=goals` must match the name you used in the tab navigation control, but _without_ the # in front. This name must be unique across the entire character edit template, so it's suggested that you use something like `myplugin-tabname`.
{% endtip %}

The markdown-editor control lets players easily edit and preview markdown text.

## Send the Data

The controls above let us *enter* the data.  To actually *send* the data to the game, there's one more place we need to wire up: the edit controller.  That lives here: `ares-webportal/app/components/char-edit-custom.js`

The controller has as an `onUpdate` method that gets activated when the player clicks the 'save' button.  In there it sets up a hash with all the profile data the player entered.  We'll add our goals to it.

    return { goals: this.get('char.custom.goals') }
    
{% tip %}
If you ever need to support multiple custom fields, you have to combine them into a single return statement.

`return { goals: xxx, other: xxx }`
{% endtip %}
