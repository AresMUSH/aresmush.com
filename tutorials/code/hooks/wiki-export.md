---
title: Custom Wiki Character Export
description: 
layout: page
tags:
- code
- custom hooks
---

> This [custom code hook](/tutorials/code/custom-hooks.html) is part of the Website plugin.


The wiki character exporter builds certain files by default (profile, background, etc.) and can optionally include a file named `other.txt` with anything specific to your game.

To do so, just update `custom_wiki_char_export.rb`:

```
    def self.custom_wiki_char_export(char)
      "OUTPUT TO PUT INTO other.txt"
    end
```

Note:

* The output needs to be a string.
* The string should be MUSH-compatible (not HTML), just like MU command output. ANSI codes will be removed during the output process.
* You cannot currently create multiple output files. Everything will go into `other.txt`. You can separate sections with linebreaks/lines.