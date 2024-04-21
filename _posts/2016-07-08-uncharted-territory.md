---
title: Uncharted Territory
date: '2016-07-08'
layout: post
description:
categories:
tags: [feature, web]
author: Faraday
preview_image: compass.jpg
teaser: A deeper look into what a MUSH web app might look like.
---

Thanks to everyone who gave feedback on the [last post](/blog/crossroads.html). It got me thinking more about what a MUSH server would look like today, without the 20+ years of history behind the genre. It wouldn’t be a telnet client, that’s for sure. It would be a web app. But what sort of web app?

So I started playing around with some ideas. Re-thinking the very foundation of how the game worked. Using online games and chat software for inspiration, I started to imagine what a text-based gaming engine would look like if you could divorce it from its telnet-driven roots.

My vision far exceeds my front-end web development capabilities and free time, but here’s a tiny sample of what could be possible:

Main game window.  The exits are clickable buttons and the character names are clickable links that could show their wiki profile. 

{% include pretty_image.html file='postpics/uncharted-web1.png' caption="Game Tab" %}


It’s still text-driven, obviously, because it’s a text-oriented game, but you can start to incorporate bits of interactive multimedia. The exits can be clickable buttons and the character names clickable links. Descriptions could embed image links and actually show them. Things can be organized into separate tabs, like the chat tab:

Channel chat is automatically separated into a different tab.

{% include pretty_image.html file='postpics/uncharted-web1.png' caption="Chat Tab" %}


It’s a step up from just having essentially a telnet window embedded in your web browser, but still not as fully-functional as a MUSH client. Not yet, anyway. There’s no reason why it couldn’t be, given enough time and effort. Even better – the back-end that supports this would also be able to support a richer MUSH client interface in the future, if anyone were so inclined.

In the mean time, this could live in parallel with existing MUSH clients. I envision a thin proxy taking the user-typed commands like p Faraday Bob=Hello. and converting them into a standard web API call with parsed data like `{cmd: page, targets: [Faraday, Bob], message: "Hello."}` From there, it would work the same as every other Rest API-driven web app on the planet.

All of this adds a fair bit of technical complexity and rework, so I’m not completely sold on the idea yet. But it’s definitely worth spending some more time on it. If they can make [Discourse](https://try.discourse.org/) work for people out of the box, with a nifty web front-end and a rich API for other clients, there’s really no reason why it couldn’t be made to work for a MUSH.