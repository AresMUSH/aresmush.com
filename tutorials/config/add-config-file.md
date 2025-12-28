---
title: Add a New Config File
layout: page
tags:
- config
---

Sometimes you need to add a brand new config file. Usually this happens when you have added some custom code.

Some requirements about config files:

- They live in the `aresmush/game/config` directory. 
- They must have the `yml` extension. (e.g., `yourpluginname.yml`)
- Their name should match the name of the plugin they belong to, though you can break up a single plugin's config into multiple files. (e.g., `yourpluginname_skills.yml`, `yourpluginname_items.yml`, etc.)
- Their contents must be a YAML hash matching the name of the plugin and contain at least one config field. For example:

```
---
yourpluginname:
  color: blue
```


There are several ways to create a new config file:

1. Upload a file using [FTP](/tutorials/code/edit-code/ftp-upload.html). 
2. Create the file using a shell editor like nano.  (e.g., `nano aresmush/game/config/myplugin.yml`) and then paste in the contents.
3. Run the following command from the `aresmush` directory:

```
bin/script add_config_file,yourpluginname
```