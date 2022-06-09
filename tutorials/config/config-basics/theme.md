---
title: Essential Config - Web Portal Theme
description: 
layout: tutorial
nextstep: config-files
prevstep: text
tutorialIndex: tutorials/config/config-basics
essentialConfigTutorial: true
tutorialName: Essential Config
tags:
- config
---

Most games will want to customize the appearance of the web portal.

{% include toc.html %}

## Using a Pre-Made Theme

Several pre-made themes are available - you can browse them in the [AresCentral Theme Directory](https://arescentral.aresmush.com/themes).

To use one of these themes, just use the command `theme/install <github url>` in your MU client. For example: `theme/install https://github.com/AresMUSH/ares-dark-theme`.

To revert to the default theme, use `theme/install default`.

## Choosing Colors

You can customize what colors are used for various elements in your theme.

1. Go to Admin -> Setup in the web portal.
2. Select "Edit Theme Colors". 
3. Use the color widgets to select the desired colors.

{% note %} 
You will need to reload the page to see the colors change.
{% endnote %}

## Uploading Theme Images

The theme uses several standard images: one across the header banner, one on the login screen, and a background used for character and scene pages.  You can upload new versions of these images.

1. Go to Directory -> Files.
2. Select the `theme_images` directory.
3. Select an image you wish to change.
4. Select "Upload Files".
5. Browse to find your new image on your PC.
6. Make sure that the file is named **exactly the same** as the original (e.g. background.png) and the "**Overwrite**" box is checked.
7. Click the upload button.

{% note %} 
Some browsers (notably Chrome) are stubborn about reloading theme images right away due to image caching.  Try viewing it in private/incognito mode to see your new images.
{% endnote %}

{% tip %}
It can be tricky sometimes to size/align your banner image the way you want it on both mobile and desktop screens.  For some tips, see [Choosing a Header Background](https://aresmush.com/tutorials/config/website.html#choosing-a-header-background).
{% endtip %}

## Advanced Theme Customizations

You can customize your theme further with custom CSS, but this is all we're going to cover for now.  See [Configuring the Website](/tutorials/config/website.html) for more information.