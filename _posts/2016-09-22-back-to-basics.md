---
title: Back to Basics
date: '2016-09-22'
layout: post
description:
categories:
tags: [feature, web]
author: Faraday
preview_image: basics.png
teaser: The harsh realities of the web interface experiment.
---

The last couple posts have been about the grand AresMUSH web experiment, exploring the practicality of a web-based Ares front-end. Having puttered around with it for a couple months, I have unfortunately concluded that it’s just not practical at this point.

A web interface would certainly make it easier to play. It would be modern and cool. But given the state of web technology and the need to support old-school MU clients, it would make it **harder** to create a game and **harder** to code, breaking two of the primary goals of Ares.

## Impracticalities

Maintaining two independent user interfaces (web and old-school MU client) takes a lot of work. It adds layers of complexity to the code, making it more of a chore to learn and maintain.

Also, web frameworks are evolving at a breakneck pace. The latest/greatest thing today might not even be around tomorrow, leading to the sorts of horror stories described in [this article](https://hackernoon.com/why-learning-angular-2-was-excruciating-d50dc28acc8a#.e6wgdmejv). WebSockets, which are pretty essential to a dynamic two-way game server, are still [dicey](https://msdn.microsoft.com/en-us/hh563510.aspx) to implement and not fully supported across all browsers.

There are other challenges in the server administration and the huge effort required to support a full-featured web MU client (logging, spawns, timers, etc.) that players would expect.

Can it be done? Sure. But if it feels like work to me, as a professional web developer, it doesn’t seem like the right avenue for hobbyist game coders and admins. Simpler feels better.

## Hope for the Future

The tooling problems, at least, will hopefully improve in time. Dynamic web applications and websockets are becoming more the norm. Rails [Action Cable](http://guides.rubyonrails.org/action_cable_overview.html) shows particular promise for Ares, given that it uses Ruby.

Ultimately I think the future is a web-only game (ditching the old-school MU clients) that you can install out of the box like most blog or forum software. Tweak a few config settings and you’re off to the races. Add a fully-managed hosting solution to take care of the admin side, and it would be even better.

Perhaps Ares can someday be the back-end engine for that sort of game. Time will tell. But that’s not the direction for Ares 1.0 (for now).

## Moving Forward

So for now, Ares is marching on with support of the old-school MU client interface. There will probably be a lightweight web console for configuring the game – something like what was described back in [Ares Web Portal](/blog/ares-web-portal.html) – but not a full-fledged web UI.

I’m hoping to have a public beta site game open by the end of the year, so stay tuned.