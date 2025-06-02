---
title: Custom Sidebar Sections
description: 
layout: page
tags:
- code
- custom hooks
---

> This [custom code hook](/tutorials/code/custom-hooks.html) is part of the Website plugin.


You can add your own section to the sidebar, right below "Game Status". (If you want to put it somewhere else, you'll have to dig into the core code.)

The files to modify:

* Define the sidebar contents: `ares-webportal/app/components/sidebar-custom.hbs`
* You probably won't need any interactive elements in the sidebar, but if you do put them in: `ares-webportal/app/components/sidebar-custom.js`
* Add the code to return data to the web: `aresmush/plugins/website/custom_web_data.rb` (In the `custom_sidebar_data` method.)

For example, your game-side function to return the data might look like this:

    def self.custom_sidebar_data(viewer)
      { your_field: your_data }
    end

Be sure to return an empty hash `{}` if you have no custom data.

This data will be available in `this.custom` inside the web component. You'll also want to wrap your sections in the same div classes as the other sidebar sections. For example:

<pre>
  &lt;div class="sidebar-box &#x7b;&#x7b;this.boxStyle}}">
    &lt;div class="sidebar-heading">
        &lt;h2>Test &lt;i class="fa fa-calendar" aria-hidden="true"></i></h2>
    &lt;/div>

    &lt;p>{{this.custom.your_field}}</p>
  &lt;/div>
</pre>

The `boxStyle` parameter is passed in so you can match the styling of the main sidebar.
