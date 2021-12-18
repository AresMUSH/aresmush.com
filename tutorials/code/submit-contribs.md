---
title: Submitting Contributions
description: 
layout: page
tags:
- code
- plugins
- extras
- contribs
---

Anyone can make plugins or themes for AresMUSH. As long as you're following the [License](https://aresmush.com/license) requirements, go to town and share what you like however you like.

If you want to take advantage of Ares' automated theme/plugin installers, and have your contributions easily found by others in [AresCentral](https://arescentral.aresmush.com), you can submit your contributions to AresCentral. This guide will tell you how.

{% note %}
However you share them, all community-developed plugins and themes fall under the same [license](/license) as the original Ares code.
{% endnote %}

{% include toc.html %}

## Sharing Plugins

In order to be compatible with the automated plugin installer, your plugin must have its own repository in GitHub. For example: [Preferences Plugin](https://github.com/AresMUSH/ares-prefs-plugin). If you need help creating one, feel free to [ask for help](/feedback.html).

To have your plugin included in the [AresCentral plugin directory](https://arescentral.aresmush.com/plugins), just [contact us](/feedback.html) with the GitHub url.

### Plugin Repo Structure

Plugin repos must follow a particular folder structure:

* The repo must be named **ares-YOURPLUGINNAME-plugin**.
* A `plugin` folder containing files organized into sub-folders matching the [Plugin Folder Conventions](/tutorials/code/plugins.html) (help, locales, etc.)
* A `webportal` folder containing files organized into sub-folders matching the web portal's `app` folder (templates, components, etc.)
* A `game` folder containing files organized into sub-folders matching the aresmush `game` folder (config, text, etc.)
* A `README.md` file explaining what the plugin does and how to use it.  You can use one of the [existing plugins](https://github.com/AresMUSH/ares-prefs-plugin) as a model.
* The installer ignores any other folders, so you can use them for examples, documentation, or whatever you want.

For example:

{% include pretty_image.html file='code/extras-dir.png' max-width="300px" %}

All folders are optional, so just omit any that don't apply to your plugin.

{% note %} 
The automated install just copies _your_ plugin's files.  It cannot handle changes to _other plugins_ (for example, adding steps to the Chargen config or Chargen web portal screen). Your README should include instructions for doing those sorts of changes manually.
{% endnote %}

### Plugin Versioning

Versioning your plugin can make it easier to troubleshoot problems by identifying whether a given game is running your latest code.  To do this, just add a "version" method to your plugin module, as shown below, and update it whenever you release new code.

```
module AresMUSH
  module Yourplugin
    def self.version
      "1.0"
    end
  end
end
```

### Plugin Database Migrations

Sometimes your plugin will need a database field initialized, or a default config value set. You could give game runners some [tinker](/tutorials/code/tinker) code snippets to run, but it can be easier to just define a method in your plugin to perform the installation steps.

For example, you might create a method to initialize a database value at install time:

```
module AresMUSH
  module Yourplugin
    def self.install_setup
      Character.all.each { |c| c.update(your_db_field: 'default value') }
    end
  end
end
```

Then you just need to tell them to run `ruby Yourplugin.install_setup` after they've installed the plugin.

{% tip %}
Installation setup is important array/hash database fields. Your model class may set a default value (`[]` or `{}`), but that only applies to _new_ characters. For existing characters, these fields will be `nil` unless you take the time to initialize them.
{% endtip %}

You can also provide something to run when the code gets upgraded.  The database migrator class has some utilities for reading/writing config files that are particularly useful here.  For instance, you might create a method that sets a new configuration option to a default value:

```
module AresMUSH
  module Yourplugin
    def self.migrate_add_someoption
      DatabaseMigrator.read_config_file("yourplugin.yml", config)
      config['yourplugin']['someoption'] = 'some value'
      DatabaseMigrator.write_config_file("yourplugin.yml", config)
    end
  end
end
```

Then you can tell game runners to run `ruby Yourplugin.migrate_add_someoption` to update their configuration.

{% note %}
Make sure all hash values in migrations use the arrow notation, **NOT** the symbol notation: 

    RIGHT: 'someoption' => 'some value'
    WRONG:  someoption: 'some value'
{% endnote %}

## Sharing Themes

In order to be compatible with the automated theme installer, your theme must have its own repository in GitHub. For example: [Ares Dark Theme](https://github.com/AresMUSH/ares-dark-theme). If you need help creating one, feel free to [ask for help](/feedback.html).

To have your plugin included in the [AresCentral theme directory](https://arescentral.aresmush.com/themes), just [contact us](/feedback.html) with the GitHub url.

### Theme Repo Structure

In order to be compatible with the automated theme installer, a theme must follow a particular folder structure:

* The repo must be named **ares-YOURTHEMENAME-theme**.
* A `styles` folder with `custom_style.scss` and `colors.scss`.
* An optional `images` folder with the [theme images](/tutorials/config/website.html) needed by the portal. You can supply all, any, or none of the images.
* A README file describing your theme.  It's nice to include some screenshots as well.

## Sharing Other Things

Code snippets, config files, and other things that are neither plugins nor themes can be posted on the [Forum](https://forum.aresmush.com) or contributed to the [Ares Extras](https://github.com/AresMUSH/ares-extras) repo.

## Submitting Patches

Coders may also submit patches to the main Ares codebase for bugfixes and/or new features using GitHub pull requests.

{% note %} 
Faraday is very picky about what code goes into the main repository. It's advisable to [ask first](/feedback.html) before embarking on major patches to the core code. You can, of course, do anything you want in your own fork or your own plugin(s).
{% endnote %}
