---
title: Making Help More Helpful
date: '2017-08-18'
layout: post
description:
categories:
tags: [feature, web]
author: Faraday
preview_image: safety.jpg
teaser: How to build a better help system.
---

MUSH help systems are generally pretty… unhelpful.

Traditional MU* help has been based around a screen of disjointed topics.

    ------------------------------------------------------------------------------- 
                                        +help Topics                                 

    +BG                       +FINGER                   +DESC
    +HELP                     +LIST                     +MAIL

    See +help  for more information about a topic.
    -------------------------------------------------------------------------------


+BG? +FINGER? If you don’t already know what these things are, this “help” is nonsensical. Your only real option is to just go through them one by one typing ‘+help xxx’ over and over again. And don’t even get me started on ‘help’ vs. ‘+help’.

One of the things I’ve tried to do with Ares is to improve the help system.

The help is very web-centric. Help topics are organized into general categories (Character Creation, Community, etc.) and each display a brief summary.

{% include pretty_image.html file='postpics/help2.png' %}


Help files are Markdown, allowing you to use all sorts of formatting (bold, tables, callouts, etc.), hyperlinks and even images.

{% include pretty_image.html file='postpics/help.png' %}


Inside the game itself, you can view the topic list organized by category, just like the web view, with links to the web portal.

{% include pretty_image.html file='postpics/help3.png' %}


In the game itself, you can get a link to the web portal using help, or use help/view to display the web text in-game.

{% include pretty_image.html file='postpics/help4.png' %}


And finally, can also do help to display a quick reference for a specific command.

{% include pretty_image.html file='postpics/help5.png' %}


I’m sure there’s still room for improvement, but at least it’s a step in the right direction.
