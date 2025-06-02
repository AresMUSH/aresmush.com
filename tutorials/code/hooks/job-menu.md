---
title: Custom Job Menu
description: 
layout: page
tags:
- code
- custom hooks
---

> This [custom code hook](/tutorials/code/custom-hooks.html) is part of the Jobs plugin.

This hook allows you to add a new item/action to the menu that appears when viewing a job.

Add the menu itself to `ares-webportal/app/components/job-menu-custom.hbs`.  

<pre>
  &lt;li><a href="#"  &#x7b;&#x7b;action 'yourAction'}}  class="dropdown-item">Your Action</a></li>
</pre>

To handle the button action, add code to `ares-webportal/app/components/job-menu-custom.js`.

      gameApi: service(),
      flashMessages: service(),
      actions: {
        yourAction() {
           // Your code
           }
        }

To pass custom data to your menu (such as a list of abilities from your custom skills system), modify the `custom_job_menu_fields` method in `aresmush/plugins/jobs/custom_job_data.rb`:

    def self.custom_job_menu_fields(char, viewer)
      abilities: YourCustomPlugin.build_abilities_list
    end
    
Custom job data is available through `this.job.custom` in the custom job menu component.
