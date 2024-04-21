---
title: Crossroads
date: '2016-05-26'
layout: post
description:
categories:
tags: [feature, web]
author: Faraday
preview_image: crossroads.jpg
teaser: Imagining a more modern version of MUSH apps. Is Ares on the right track?
---

Sorry for the lack of updates, but I was eaten by RL for awhile and haven’t had much chance to work on Ares. I’m slowly getting back into it.

Where do things stand? Well, I feel like I’m at a design crossroads.

Ares has always had three goals:

* Make it easier to create a game.
* Make it easier to play (while not alienating veteran MUSHers).
* Make it easier to code.

The current incarnation of Ares has done that, I think. The alpha test game went well, and [AresCentral](https://arescentral.aresmush.com) has been running stably for over a year.

But it doesn’t feel like enough. I’ve made things easier, but haven’t made them easy. So I ask myself: Am I on the right track?

## Field of Dreams

Wouldn’t it be cool if MUSHes worked like any other software-as-a-service web app in the world? You go to mushhost.com, create an account, tweak some settings through a nifty web UI, maybe install some plugins, and start building your game. Other players go to yourmush.com and use the nifty web UI to play. Your app is updated to the latest version behind the scenes when bugfixes and new features are released. If you’re really adventurous, you can create your own plugins.

That would be pretty freaking awesome if you ask me. (Well, maybe except for playing through a web UI, but we’ll get back to that…)

And it’s all completely possible. The stuff I did for the [Ares Web Portal](/blog/ares-web-portal.html) prototype just scratched the surface of what the technology is capable of. Sometimes I tell myself, “If you build it, they will come.”

But will they?

Some new players might be drawn in by a platform like this, but who’s going to build games for them? Who’s going to play with them? Show them the ropes?

It has to be the veterans. Dinosaurs like me who have been MUSHing for years and have very strong opinions about how things should be done.

But in a community where people boycott games based on what channel commands they use and fight holy wars over which MUSH client is better, is it reasonable to expect that they’ll welcome a web-based MUSH platform that works very differently?

Color me dubious.

## A Game of Tradeoffs

The other basic problem is that things that make using the game easier also make *administering and installing* the game harder.

Your nifty web UI now requires a fistful of tools working together and a full-stack web developer to change them. And oh-by-the-way, instead of a little MUSH shell account you now need a VPS with root privileges and a web server. Hope you have someone to manage the security updates.

So while the web app thing sounds good on paper, maybe it’s not the right goal. Maybe we need something simpler. Easier to manage. Maybe we need to take a baby step towards the future instead of a leap off a cliff.

I don’t know. So for now, I stand at the fork in the road and ponder.
