---
title: Custom FS3Combat Actions
description: 
layout: page
tags:
- code
- custom hooks
---

> This [custom code hook](/tutorials/code/custom-hooks.html) is part of the FS3Combat plugin.

Creating your own combat actions takes a fair amount of custom code.  But once you have them, you can easily [register them](https://aresmush.com/tutorials/code/fs3-roadmap.html#adding-a-new-action) with the combat system.

You can register your own custom combat actions in `plugins/fs3combat/custom_hooks.rb` in the `custom_actions` method. This acts as a sort of mini dispatcher for combat actions.  

For example, to add a new "Jedi mind trick" action named 'combat/mindtrick' with an action class named `MindTrickAction`, you would do:

    def self.custom_actions
       {
          'mindtrick' => MindTrickAction
       }
       

## Action Class

To implement your action, you'll need a class (such as `MindTrickAction` above) that inherits from `CombatAction` and implements the required methods:

* `prepare` - Parses arguments and performs error checking.
* `print_action` - Formats the action summary for an emit.
* `print_action_short` - Formats the action summary for the combat HUD.
* `resolve` - Handles combat resolution.

These are described more below.

{% note %}
Each instance of a combat action class is created when the character chooses the action, and will hang around until the character chooses a different action. That means it will potentially last across multiple turns.
{% endnote %}


### prepare

The `prepare` method is done when you first choose the action. It will perform the necessary error checking and set up variables for later.

Prepare will return either an error message (which is shown to the player) or `nil` if everything is OK. If it returns an error, the action is aborted and the character's prior action remains unchanged.

For example, in MindTrickAction this might:

1. Check that the acting character is a Jedi.
2. Check that the target is valid.
3. Store the target combatant in a class variable for later.

### print_action

If the action passes the 'prepare' stage, a message is emitted to combat. The `print_action` method formats the emit.

For example, in MindTrickAction the long action text might look like: "Anakin will try a mind trick on Stormtrooper1 this turn."

### print_action_short

Similar to `print_action`, this method summarizes the action in short text for the combat HUD. 

For example, the MindTrickAction short action text might look like: "MindTrick Stormtrooper1". (Remember, it shows up next to Anakin's name in the HUD so it's already clear who's doing it.)

### resolve

The `resolve` method is called when it's the player's turn to act, and actually figures out what happens. It returns a **list** of messages, which will be emitted to the combat. Even if there's only a single message, you must format it as a list, like `return [ message ]`.

You may need to redo error checking that happened during `prepare`, since conditions may have changed. 

Conditions that can't change, for example:
- Needing a certain skill (you can't lose skills in FS3)
- Needing a certain weapon (changing weapons would reset your action)

Conditions that might change, for example:
- The target may have been KOed or left combat.
- The target's condition may have changed (e.g., if you were trying to rally them, they might have hero'ed themselves)

Your resolve method will usually make the necessary skill rolls and inflict damage/onditions upon the target. Return an indication of success or failure in the response message(s), 

For example, the MindTrickAction might return something like:  `[ "Anakin mind tricks Stormtrooper1 successfully." ]` (remember that it needs to be a list.)