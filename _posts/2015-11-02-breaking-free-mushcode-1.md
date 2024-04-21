---
title: Breaking Free from MUSHCode - Part 1
date: '2015-11-02'
layout: post
description:
categories:
tags: [feature, code]
author: Faraday
preview_image: mushcode1.jpg
teaser: Why Ares moved away from softcode.
---

In existing MUSH servers, **Hardcode** is the core distribution, usually C or C++. Changing it requires shutting down the game and recompiling the code, and it's not really designed for extensibility. **Softcode** (aka **MUSHCode**) is a highly-flexible scripting language that players can edit "live" from the game console.

I really admire the authors of MUSHCode for creating an immensely powerful scripting language using '80's era programming tools. It was fine in the days when people were scripting [Falcon Controllers](http://www.groundline.net/eu-mush/mushman/) and Vending Machines, but it has some serious flaws when you try to adapt it to the kind of mammoth skills, space and economy systems MUSHCoders are doing these days.

## It's a Mess

Trying to squish complex code onto a single command-line driven interface without whitespace, variables or comments can be pretty painful.

    [u(fun_mod_combatstat,%0,action,[lcstr(trim(%1))])]
    [u(fun_mod_combatstat,%0,target,[iter(%2,[unprettify(trim(##))],\,,\,)])][u(fun_mod_combatstat,%0,actoptions,
    [iter(%3,[trim(##)],\,,\,)])][localize([setq(0,u(fun_combatstat,%0,subduing))][switch(t(%q0),1,switch(%1,subdue,,
    [u(fun_mod_combatstat,%0,subduing,)][u(fun_mod_combatstat,%q0,subduedby,)]))])][u(fun_combat_msg,
    [prettify(lcstr(%0))] will [switch(%1,explode,use a [u(fun_combatstat,%0,weapon)] this turn. [capstr_all(lcstr(%2))]
    is right next to the explosion[switch(t(%3),1,%Band [capstr_all(lcstr(%3))] is nearby)].,[lcstr(%1)]
    [switch(%2,,,%B[prettify(lcstr(%2))])] this turn.[switch(t(%3),1,%BOptions: %3)])][u(fun_add_id,%0)])]
    [set(me,acted:[setdiff([v(acted)] %N,)])][switch(u(fun_everyone_acted),1,u(fun_org_msg,[ansi(hc,Everyone has
    entered their actions.)]))]

Yeah. Good luck figuring out what *that* does. And that's just **one** function out of hundreds in my FS3 combat system.

I've shown MUSH code to my software colleagues and the reaction is either hysterical laughter or a disbelieving "WTF?!!?".

## Nobody Knows It

I'm going to guess there are no more than a dozen "master" MUSHCoders out there. It's an obscure, difficult-to-learn programming language. MUSHCoders are notoriously in short supply, and the lack of a coder is one of the leading reasons why a new game never gets off the ground.

## It's Fragile

Partly this is tied to the "messy" problem. Changing existing MUSHCode is like juggling spaghetti. But more than that - editing complex code live on a command line is just a really bad idea. You're bound to break something, and when you do - the players are immediately affected. You're also lacking any form of revision history to know what changed. Once you touch something, the old code is gone. Nobody codes that way in the real world.

## It's Not as Necessary as It Once Was

The great power of MUSHCode was that any player could code from the game console. Bob could make his own personal multi-descer or notepad object. A team of coders could control all of the game's MUSHCode without you needing to give them all access to the game server.

While there are still die-hard players who want to do their own code, a lot of games now disallow personal coding for security or philosophic reasons. Even on games that allow it, most players just can't be bothered.  As for server security?  Commonly your one-and-only coder is also the techie who manages the server stuff anyway.

## A Different Way

There are some games where these limitations aren't a problem. Maybe you're lucky enough to have a master MUSHCoder on staff, or someone who's willing to learn. Maybe your coder uses an offline code formatter and test server so they can test code changes before implementing them on the live server. Maybe you absolutely need to allow players to do their own scripting, or can't trust your coder with the keys to the server kingdom.

If any of that applies to you, the existing MUSH servers are probably a good fit.

But for many games, AresMUSH provides a different way to code, without MUSHCode or any sort of scripting from the game console. In the next blog post, I'll talk more about what Ares does instead.