---
title: Reinventing the Wheel
date: '2018-09-08'
layout: post
description:
categories:
tags: [code]
author: Faraday
preview_image: cart.jpg
teaser: How to get started coding in Ares.
---

There’s not much new to report on the Ares development front. Feedback from the always-helpful beta testers has resulted in a few fixes and features, and I’ve filled in some gaps in the tutorials. Everything is swell!

The thing that people still seem to struggle with is coding systems for their games. I hear questions like: “How can I rewrite FS3 to support Pacific Rim mechs?” or “How can I do D20 chargen?”

I get the temptation to jump into the deep end. I really do. Ares comes with so much built-in infrastructure that often the only things left to code are the “big systems” like skills/space/economy.

But here’s the thing… you wouldn’t jump onto a PennMUSH game for the very first time, rub your hands together, and say, “Today, I’m going to learn MUSHCode. Let’s start with D20 chargen!” Or jump into iOS development and on the first day expect to code Angry Birds. Right?

The trick to learning any software is to start with something small and work your way up. For Ares code, my suggestion would be:

* Do the [Basic Coding Tutorials](http://aresmush.com/tutorials/code). They will answer many of your questions, I promise. If something’s not clear – don’t hesitate to ask for help.
* Take a simple existing plugin, like ‘who’, dissect the code to see how works, and then build it from scratch all your own. If you can’t figure out what it’s doing, ask for help.
* Take an existing command and make a simple extension or change to its behavior.
* Try to make a new command.

Rinse and repeat until you’re pretty comfortable with how things work. Only then will you be able to design a complex plugin like “Shadowrun chargen” from scratch.

It may seem like busy work, doing exercises and building things that have already been done. But it really is an effective way of learning software. I wrote the following passage in [Practical MUSH Coding](https://aresmush.com/articles/practical-mush-coding/) over a decade ago, and it’s every bit as true for Ares coding as it was for MUSHcode:

> I believe strongly that the only way to learn to code is by doing it. No amount of reading and theory that can substitute for the experience you get by working on even a small code project. Unfortunately, most of the small projects have been done already. +who, +finger, bulletin boards – every MUSH in the world has them. Why reinvent the wheel, if someone’s already done the work?
> 
> Because that’s how you learn. +finger is a fairly trivial task, but it’s practice. It reinforces the basic principles used in coding. If you code little things like that often enough, you’ll be able to do them in your sleep. Only then will you be able to tackle tasks like a full-blown combat system.

Happy coding!