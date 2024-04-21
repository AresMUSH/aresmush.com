---
title: Breaking Through
date: '2017-04-06'
layout: post
description:
categories:
tags: [feature, web]
author: Faraday
preview_image: breakthrough.jpg
teaser: Finding a happy compromise for web-based configuration.
---

For the past few months, I’ve been struggling with two competing goals of AresMUSH: make it easy to set up, and make it easy to create custom code. Easy setup leads you to a web-based system, but a good web-based system adds a ton of complexity to the code base and makes it much harder to customize the code. Catch 22, right?

After going round and round and round and round and… I **finally** found a happy compromise.

The most basic game config will now have dedicated screens in the Web Portal, making minimal customization super easy. For example, here’s a screen to edit the basic game information.

{% include pretty_image.html file='postpics/webconfig.png' caption="Web Config" %}


And here’s a screen to edit the FS3 Skills list:

{% include pretty_image.html file='postpics/webconfigfs3.png' caption="Web Config (FS3)" %}


That’s all well and good, but what about the rest of the configuration? I didn’t want to force plugin designers (or myself) to create a web config screen for every single plugin. But without that, configuring the plugins required you to connect to the server shell and edit config files in emacs. Yuck.

The solution was to make a system that’s reasonably easy but also generic – so it can work for any plugin. Happily, I found a web-based file editor module. So now you can use the Web Portal to edit any plugin config file in a spiffy editor with syntax highlighting and indentation help:

{% include pretty_image.html file='postpics/webconfigedit.png' caption="Web Config Editor" %}


You’ll still need to connect to the server shell if you want to change the source code, but if you’re running the standard code you should be able to do everything you need from the Web Portal. I think this goes a long way to making Ares work for someone without any coding experience and overcomes one of the chief obstacles that’s been plaguing me.