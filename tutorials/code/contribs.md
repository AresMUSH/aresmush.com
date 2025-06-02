---
title: Community Contributions
description: 
layout: page
tags:
- code
- plugins
- extras
---

Community Contributions include plugins and themes that are not part of the standard Ares install.

{% include toc.html %}

## Finding Contribs

You can find contributions on AresCentral:

* [AresCentral Plugin Directory](https://arescentral.aresmush.com/plugins)
* [AresCentral Theme Directory](https://arescentral.aresmush.com/themes)

## Installing Plugins

You can install a plugin directly from the game using `plugin/install <github url>`. For example:  `plugin/install https://github.com/AresMUSH/ares-prefs-plugin`.

{% note %} 
1. Make sure the plugin is compatible with your version of AresMUSH.  Most require the latest version.
2. Many plugins require some additional manual install steps.  Be sure to check the README file in each plugin's folder for detailed information on installation and configuration.
3. Use community plugins at your own risk. They are not officially supported (unless otherwise specified).
{% endnote %}

## Installing Themes

You can easily install new themes for your web portal by using `theme/install <github url>`. For example: `theme/install https://github.com/AresMUSH/ares-dark-theme`.
  
To restore to the default theme, use `theme/install default`.

## Updating Plugins

As long as you haven't modified the plugin's source code, you can upgrade it just by using the `plugin/install <github url>` script again.  This will replace the code files with the newest ones.  Your configuration will not be affected.  The release notes will tell you if you need to make any additional config or code changes by hand after the upgrade.

> <i class="fa fa-exclamation-triangle"></i> **Warning:** Do not re-install a plugin if you've got custom code modifications, as this will overwrite your changes. You'll have to do the upgrade by hand.  GitHub's version compare tools can help you figure out what changed. You could even make your own 'fork' of the extra repo to manage your code changes and take advantage of GitHub's merging features. Feel free to ask for help.

## Uninstalling Plugins

Ares plugins plug IN easily, but taking them OUT again requires a bit of code fiddling. Some plugins have more detailed uninstall instructions in their README file, but in general you need to:

1. [Remove the plugin's database fields]({{site.baseurl}}/tutorials/code/db-remove-field.html) and wipe the data and any associated database objects. 
  * Many plugins have instructions to help you do this. See the plugin's README for details.
2. Remove the code from your game server (and GitHub fork, if applicable).  This includes:
  * the plugin directory (`aresmush/plugins/myplugin`)
  * the config files (`aresmush/game/config/myplugin_*.yml`)
  * the web portal files (these vary by plugin - see the plugin repo for details)
  * any modifications to [custom code hooks]({{site.baseurl}}/tutorials/code/index.html#custom-code-hooks) that reference the plugin
4. Remove the plugin from the extras list in the `plugins.yml` config file. If you now have no extras, make it an empty list: `[]`.
5. [Restart the game server]({{site.baseurl}}/tutorials/manage/shutdown.html).

This can be an involved process, so don't hesitate to [ask for help](/feedback.html) if you need it.

## Contributions

See [Submitting Contributions](/tutorials/code/submit-contribs.html) if you want to contribute your own plugins or themes.