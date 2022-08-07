---
title: Plugins
description: 
layout: page
tags:
- code
- plugins
---

Ares supports a robust **Plugin** system, with its features separated into plugin modules.  Plugins provide all of the player commands - even core functionality like movement, help, descriptions, pages and channels.  They handle game events, responding to things like "character connected" or "game started".

{% include toc.html %}

## Folder Organization

Each plugin has its own folder inside aresmush/plugins. The name of the folder is the name of the plugin.

{% note %} 
The folder name must be one word, all lowercase, with no special characters.
{% endnote %}

There's a standard organization to a plugin folder.

    myplugin
        - commands (command handlers)
        - events (event handlers)
        - help* (help files)
        - locale* (translation files)
        - public (models and interfaces used by other plugins)
        - templates (templates and renderers)
        - web (web request handlers)
        myplugin.rb

Help and Locale must be in separate folders, but the other folders are optional.  You could lump everything under `myplugin` if you want, but the standard organization will make it easier to find files - particularly in large, complex plugins.

## Plugin Modules
All plugin code lives in its own Ruby module - inside the main AresMUSH module - to keep the code organized and provide clues as to what goes where.

    module AresMUSH
       module MyPlugin
       end
    end

**Important Conventions:** 

1. The module must be defined in a file matching your plugin folder name, located in the top level of your plugin folder.
2. The module must be nested within the main AresMUSH module.
3. The name of the Ruby module must match the name of the plugin folder when converted to lowercase.  In other words, it's okay to have a module FS3Skills and a folder fs3skills.

The plugin module must define a single method:  `plugin_dir` that always returns the current folder.  For example:

    module AresMUSH
      module MyPlugin
        def self.plugin_dir
          File.dirname(__FILE__)
        end
      end
    end

There are several other optional methods that plugins can define:

* `shortcuts` - Returns the plugin's shortcut configuration.  Usually `Global.read_config('myplugin', 'shortcuts')`
* `load` - Any special actions you want to do when the plugin is loaded.  For example, the help plugin initializes some variables.
* `get_cmd_handler`, `get_web_request_handler`, `get_event_handler` - Define handlers, as explained below.

## Shared Helpers

You might find yourself doing the same thing across multiple commands within your plugin. In this case, you'll probably want to create a shared method to avoid duplicating code.

A shared method doesn't live in any individual command class; instead it lives in the plugin's module. For example:

    module AresMUSH
      module Bbs
        def self.can_manage_bbs?(actor)
          ...
        end
      end
    end

You access shared methods using the module name.

    Bbs.can_manage_bbs?(enactor)

You can place helpers anywhere, but the standard Ares code convention is to put them in the plugin folder and name them `helpers.rb`.

## Plugin Interfaces (APIs)

The plugins talk to each other through database fields and interface methods (api's).

For example, the Scenes plugin provides the interface method `Scenes.add_to_scene()`, which is used by various utilities (like skills and combat) to add system messages to a scene.  The Ranks plugin provides a database model field so you can do `character.rank`.

Methods that are intended to be used across plugins are by convention placed in the plugin's `public` folder.

## Adding and Removing Plugins

Plugins are designed to plug **in** easily, so you can add new code systems with ease.  They're also designed like puzzle pieces, so you can swap in a different version as long as it's the same basic shape.  In code terms, this means as long as it implements the same **Interfaces** as described above.

For example:  The mail API provides to main interfaces:  an `unread_mail` count and a `send_mail` method.  You can drop in any mail system you want, and everything will work just fine as long as it provides its own implementation of those methods.

Removing a plugin completely is another story.

Some optional plugins can simply be disabled through the game configuration.  See [Enabling and Disabling Plugins](/tutorials/config/plugins.html).

For others, though, it takes some code surgery.  You'll need to hunt through the code looking for all references to its models and interfaces.  You'd also have to [remove the fields](/tutorials/code/db-remove-field.html) from the database itself.  

This can be a pain, yes, but such is the price for having a fully-integrated MUSH-in-a-box system.