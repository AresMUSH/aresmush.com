---
title: Custom Scene Buttons
description: 
layout: page
tags:
- code
- custom hooks
---

> This [custom code hook](/tutorials/code/custom-hooks.html) is part of the Scenes plugin.

## Pose Buttons

Below the pose editor in a live scene is a row of buttons including "Add Pose" and "Add OOC".  With custom code, you can add custom buttons here that make use of the contents of the scene pose window--for instance, for sending a text message.

Add the button itself to `ares-webportal/app/templates/components/live-scene-custom-scenepose.hbs`.  

<pre>
  <button &#x7b;&#x7b;action 'addTxt'}} class="btn btn-default">Send Txt</button>
</pre>

To handle the button action, add code to `ares-webportal/app/components/live-scene-custom-scenepose.js`.

      gameApi: service(),
      flashMessages: service(),
      actions: {
        addTxt() {
           // Code to send the text.
           }
        }

## Play Menu Buttons

You can also add new menu items to the live scene's "Play" menu with custom code. You might do this if you're designing a new "extra" for a skill system, for instance.

Add the menu item itself to `ares-webportal/app/templates/components/live-scene-custom-play.hbs`.  

<pre>
&lt;li><a href="#" &#x7b;&#x7b;action 'giveCookies'}}>Give Cookies</a></li> 
</pre>

To handle the menu action, add code to `ares-webportal/app/components/live-scene-custom-play.js`.

      gameApi: service(),
      flashMessages: service(),
      actions: {
        giveCookies() {
           // Code to give cookies.
           }
        }

## Custom Scene Data

Sometimes your scene pose buttons or menus may require custom data, such as an ability list for your custom skills plugin. You can pass custom scene data by modifying `aresmush/plugins/scenes/custom_scene_data.rb` and returning data from the `custom_scene_data` method.

Custom scene data is available through `this.custom` in the following components:

* live-scene-custom-play
* live-scene-custom-scenepose
* char-card-custom