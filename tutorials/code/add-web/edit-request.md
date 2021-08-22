---
title: Modifying the Edit Request
description: 
layout: tutorial
nextstep: modify-chargen
prevstep: edit-template
tutorialIndex: tutorials/code/add-web
addWebTutorial: true
tutorialName: Modifying the Web Portal
tags:
- code
- website
---

Everything we added so far lets us *view* our goals on the web portal, but what if we want to edit them too?  This requires us to modify another pair of web requests.

## Edit Request

The edit request is used when someone wants to edit a character's profile.  It supplies the data for editing, which is subtly different from the data for viewing.  In particular, we use a *different* helper when formatting markdown data for input instead of output.  This helper converts %R's to linebreaks, but leaves ansi codes alone.

Edit `aresmush/plugins/profile/custom_char_fields.rb` and modify the `get_fields_for_editing` method.

      def self.get_fields_for_editing(char, viewer)
        return { goals: Website.format_input_for_html(char.goals) }
      end

## Edit Save Request

There's a separate web request when the user clicks the 'save' button on the web portal.  This handler does the actual *updating* of the character data.  We can use *yet another* helper method to format our input for MUSH.  This converts line breaks back into %r's and does a few other things to make the website entry suitable for storage.

Edit `aresmush/plugins/profile/custom_char_fields.rb` and modify the `save_fields_from_profile_edit` method.

      def self.save_fields_from_profile_edit(char, char_data)
        char.update(goals: Website.format_input_for_mush(char_data[:custom][:goals]))
      end

{% tip %} 
Though it's not covered by this tutorial, note that the web request handlers calling these code hooks check things like whether the user is logged in and has access to edit the character.  Always be sure to check permissions in your web requests.
{% endtip %}


## Testing All Our Changes

Now that we have everything wired up, we can test it out!

The easiest way to test web changes is to run the website in [debug mode](/tutorials/code/debug-mode.html).  This spins up a second copy of the website on a different port for testing.  The advantage is that changes to the web code will be immediately loaded without needing to wait for a deploy, and without potentially messing up your main site.  

But if you don't want to deal with that, you can just use the `website/deploy` in-game, or the "Redeploy Website" button on the web portal (under Admin->Manage) to deploy your changes to your real web portal.
