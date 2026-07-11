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

Add the button itself to `ares-webportal/app/components/live-scene-custom-scenepose.hbs`.  

<pre>
  <button &#x7b;&#x7b;action 'addTxt'}} class="btn btn-default">Send Txt</button>
</pre>

To handle the button action, add code to `ares-webportal/app/components/live-scene-custom-scenepose.js`.

```
      gameApi: service(),
      flashMessages: service(),
      actions: {
        addTxt() {
           // Code to send the text.
           }
        }
```

If you need data for your custom buttons, see [Custom Scene Data](#custom-data).

## Play Menu Buttons

You can also add new menu items to the live scene's "Play" menu with custom code. You might do this if you're designing a new "extra" for a skill system, for instance.

Add the menu item itself to `ares-webportal/app/components/live-scene-custom-play.hbs`.  

<pre>
&lt;li><a href="#" &#x7b;&#x7b;action 'giveCookies'}}>Give Cookies</a></li> 
</pre>

To handle the menu action, add code to `ares-webportal/app/components/live-scene-custom-play.js`.

```
      gameApi: service(),
      flashMessages: service(),
      actions: {
        giveCookies() {
           // Code to give cookies.
           }
        }
```

If you need data for your custom buttons, see [Custom Scene Data](#custom-data).
        
## Play Menu Buttons

You can also add new menu items to the live scene's "Play" menu with custom code. You might do this if you're designing a new "extra" for a skill system, for instance.

Add the menu item itself to `ares-webportal/app/components/live-scene-custom-play.hbs`.  

<pre>
&lt;li><a href="#" &#x7b;&#x7b;action 'giveCookies'}}>Give Cookies</a></li> 
</pre>

To handle the menu action, add code to `ares-webportal/app/components/live-scene-custom-play.js`.

```
      gameApi: service(),
      flashMessages: service(),
      actions: {
        giveCookies() {
           // Code to give cookies.
           }
        }
```

If you need data for your custom buttons, see [Custom Scene Data](#custom-data).

## Play Menu Sidebar

You can add custom contents to the bottom of the play screen sidebar.

Add the sidebar display to `ares-webportal/app/components/play-sidebar-custom.hbs`.  

For example, to add a 
<pre>
&lt;li><a href="/wiki/scenes" &#x7b;&#x7b;>Scene Guidelines</a></li> 
</pre>

Any action handler code can go in `ares-webportal/app/components/play-sidebar-custom.js`.  

If you need data for your custom buttons, see [Custom Scene Data](#custom-data).

<a name="custom-data" class="anchor"></a>

## Custom Scene Data

Sometimes your scene pose buttons or menus may require custom data, such as an ability list for your custom skills plugin. You can pass custom scene data by modifying `aresmush/plugins/scenes/custom_scene_data.rb` and returning data from the `custom_scene_data` method.

Custom scene data is available through `this.custom` in the following components:

* live-scene-custom-play
* live-scene-custom-scenepose
* char-card-custom
* play-custom-sidebar (as this.model.custom)