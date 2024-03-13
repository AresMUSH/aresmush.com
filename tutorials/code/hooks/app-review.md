---
title: Custom Chargen App Review
description: 
layout: page
tags:
- code
- custom hooks
---

> This [custom code hook](/tutorials/code/custom-hooks.html) is part of the Chargen plugin.

The standard chargen ensures that values are _set_, but doesn't do much to see if the values _make sense_ (i.e. that commoners can't be knights or that civilians shouldn't have Pilot Fighter Jet).  Doing these kinds of checks requires custom code, and there's a built-in hook where you can put that code.  

{% include toc.html %}

## Adding a Custom Check

Edit `aresmush/plugins/chargen/custom_app_review.rb` and make the `custom_app_review` method do whatever checks you want.

For example, if we wanted to restrict the 'knight' position to nobles, we could do:

    def self.custom_app_review(char)
      faction = char.group("Faction")
      position = char.group("Position")
      
      if (position == "Knight" && faction != "Noble")
        msg = "%xrOnly nobles can be knights.%xn"
      else
        msg = t('chargen.ok')
      end
      
      return Chargen.format_review_status "Checking groups.", msg
    end

{% tip %} 
Custom app review doesn't actually _prevent_ someone from choosing stupid values, it just flags it on the app review screen.
{% endtip %}

## Multiple Checks

If you have multiple things to check, you can concat them together into a single string. For example:

    def self.custom_app_review(char)
      faction = char.group("Faction")
      position = char.group("Position")
      
      messages = []
      error_found = false
      
      if (something)
        messages << Chargen.format_review_status("Something", "Something's Wrong")
      else
        messages << Chargen.format_review_status("Something",  t('chargen.ok'))
      end
      
      if (something)
        messages << Chargen.format_review_status("Something Else", "Something's Wrong")
      else
        messages << Chargen.format_review_status("Something Else",  t('chargen.ok'))
      end
      
      return messages.join("\n")      
    end


## Formatting Status Checks

Notice how we're using the `format_review_status` helper.  This is how most of the lines in the app review are formatted.  It will display like this:

    Checking groups.                                  Only nobles can be knights.

The Chargen helper has several built-in status values:

**Green (OK)**

    t('chargen.ok')  --> < OK! >

**Yellow (Warnings)**

    t('chargen.are_you_sure', :missing => "Field Name")       < Missing Field Name >

**Red (Errors)**

    t('chargen.too_many')                                < Too Many! >
    t('chargen.not_enough')                              < Not Enough! >
    t('chargen.not_set')                                 < Not set! >
    t('chargen.oops_missing', :missing => "Field Name")  < Oops! Missing Field Name >

You are not limited to these, of course, but using the standard that people are familiar with will help players to understand your system.