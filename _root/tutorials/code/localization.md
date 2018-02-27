---
title: Localization
description:
layout: page
tags: 
- code
- localization
---

Ares is designed for non-English games too.  All of the game code can be translated into other languages simply by swapping in different translation files, called a **Locale**.

## Locale Files

Global locale files (which are shared across many plugins) live in the `aresmush/game/locales` folder.   Plugin-specific locale files live in their respective plugin folder under a `locales` sub-folder.

A locale file looks something like this:

    en:
        dispatcher:
            huh: "Huh? Unrecognized command."
            not_allowed: "You are not allowed to do that."
        db:
            object_not_found: Nothing found with that name.

## Translation Keys

A translation key is in the form `section.key_name`.  For example:  `dispatcher.huh` or `db.object_not_found`.   You can use translation keys in the globally-available translate method `t()` to get the actual text for that key in the current language.

For example:  `t('dispatcher.huh')` would return "Huh?  Unrecognized command." in English.  In German, it might be "Bitte?  Befehl ist nicht bekannt."

> **Tip:** The game picks the appropriate language based on the global locale setting.  Individual players can't pick their own languages.
 
## Backup Locale

The localization system supports a fallback if a string can't be found in the current language.  For example - if there's no translation for "dispatcher.huh" in the German locale files, it will fall back to the English version.

## Translation Parameters

Many translations change depending on the situation, and the words may appear in a different order in different languages.  To support this, the translation method can accept parameters and put them into the translated string in different places.  For example, assume the locale file had a translation like this:

    website_address: "Visit %{portal} to access the game's Web Portal."

The URL for the web portal must be passed in via the `t()` method.

    t('webportal.website_address', :portal => 'http://www.aresmush.com')

This will result in the final string:  "Visit http://www.aresmush.com to access the game's Web Portal."

## Command Names

Localization doesn't apply to command names. This generally seems to be the standard in the gaming industry, but your mileage may vary. The "who" command will always be "who" no matter the language. You can create localized [shortcut](/tutorials/code/shortcuts) if you want to alias a command to a different name, but once you start adding in switches and other options, that's probably going to get unwieldy. If you are running an international game and find that this is a dealbreaker, please provide [Feedback](/feedback).