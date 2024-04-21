---
title: Never Say Never
date: '2016-12-23'
layout: post
description:
categories:
tags: [feature, web]
author: Faraday
preview_image: welcome.png
teaser: Maybe I was too hasty in nixing the grand web app experiment.
---

[Not too long ago](/blog/back-to-basics.html), I nixed the idea of incorporating a web server into Ares because it would increase the code complexity too much.

But as I embarked on a project to make the game setup easy for people with limited technical experience, I quickly realized that a web configuration tool was absolutely essential.

Right now Ares uses plain-text configuration files on the server itself, similar to the connect.txt and mush.cfg files of PennMUSH and TinyMUX. That’s great for programmers, but “telnet into the game shell and edit this file on the command line” is pretty off-putting for a generation who’s never had to use a C: prompt.

I briefly toyed with the idea of making everything configurable through in-game commands. That would work for some plugins, but you’d need insane commands to tackle the complex ones like FS3 and groups.

So I needed a web server to configure the dang thing. And once I had that, well… why stop there?   I shamelessly stole some ideas from [Evennia’s](http://www.evennia.com/) web UI.  For players, there’s a browser game client, web-based FS3 chargen, online help files and a character directory.  Admins can access the configuration pages and some utilities like viewing logs and shutting down the game.

Some of the screens are still rough, but that can be improved over time.  It’s still pretty nifty, in my terribly biased opinion.

Check out some initial screenshots:

{% include pretty_image.html file='postpics/welcome.png' caption="Welcome Screen" %}

{% include pretty_image.html file='postpics/play.png' caption="Play Screen" %}

{% include pretty_image.html file='postpics/chargen1.png' caption="Chargen Screen" %}

{% include pretty_image.html file='postpics/chargen2.png' caption="Chargen Screen (ctd.)" %}

{% include pretty_image.html file='postpics/admin.png' caption="Admin Screen" %}

{% include pretty_image.html file='postpics/config.png' caption="Config Screen" %}
