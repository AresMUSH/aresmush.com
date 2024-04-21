---
title: Large Scale System Design
description: A guide for building large-scale MUSH softcode systems.
layout: story
author: Faraday
---

{% note %}
This is a very old article written for PennMUSH, not AresMUSH, and its principles are pretty dated. It is archived here for posterity.  For AresMUSH code tutorials, see the [code](/code) section.
{% endnote %}

Awhile back, I wrote an article about how to design large-scale softcode systems.  It was based on the "Waterfall" model of software development.  Since then, I've come to learn a lot more about Agile software development practices, which are a much better way to go about doing things.  This new version of the article talk about how to adapt Agile practices to the design of large-scale MUSH systems.

## The Epic

Usually you'll start with some pretty big ideas:  Skills.  Chargen.  Economy.  Rooms.  

These are daunting tasks.  They're huge.  They're so huge they're *Epic*.

Epics are a good place to start, but you're not going to do any concrete work at this level.  You need to break it down further into manageable chunks.  

Why have Epics at all?

* It helps you organize the "big picture" of your game.
* It helps you to start thinking about how your systems work together.  Will the Economy system need certain skills?  Will the Room code interact with Economy to charge money for skills?
* It's satisfying when all the littler chunks come together and one of the Epics is Done.

## The Story

*Stories* are a way to break your Epics into manageable chunks.  A story is written in the form:

> As a (type of customer) I need (something they need -- from THEIR perspective).

I use "customer" loosely to refer to the players and staff of your game.  The idea is to get into the heads of your customers and understand what they're trying to accomplish.  Code exists to meet a need; it doesn't exist for its own sake.

Consider the Chargen epic.  It may spawn a bunch of stories:

* As a player, I need to set my character's demographic information.
* As a player, I need to set my character's skills.
* As a player, I need to set my character's background.
* As a player, I need to submit my background for approval.
* As a staffer, I need to review submitted backgrounds.
* etc.  (there are probably some others... handling backgrounds, accepting terms of use, and so forth, but this is enough to give you the general idea).

## The Details

When you go to work on a story, you need to flesh it out a bit more.  Software engineers call this *acceptance criteria*, but that's just a fancy way of saying:  "What do we need to do before this story can be considered 'done'."  

For a MUSH system, a good place to start is the help file.  Put yourself in the mind of the person using this system.  How will they interact with it?  What commands will there be?  What will those commands do?   How will the data be stored?

Consider the story:  "As a player, I need to set my character's demographic information."   Think about the help file in the chargen room:

> In this room, you will set up some basic info about your character's background - how old he is, his job, etc.
>         +fullname <full name>
>         +age <age>
>         @sex me=<male or female>
>         @desc me=<description>
>         &SHORT_DESC me=<short desc> - Shows up in room list.
>         +position <position> (freeform - pick your own)

You can see here that we've made a few key assumptions, using built-in MUSH commands for @sex and @desc, using a plain old attribute for shortdesc.  

This is also the point at which we start thinking about limits.  Are there any limits on fullnames?  On ages?  On positions?

Boiling all that down, we get the following acceptance criteria:

* Let the player set their full name as a free-form text field.
* Let the player set their age as a number between 18 and 80.
* Set a random birthdate (month/day).
* Tell the player they can +request to choose a different birthdate if they want.
* Let the player set their position as a free-form text field.

Note that we could've done these details differently (like letting the player enter a birthdate rather than an age) and still met the *need* of this story.  

Also note that we could have broken up this story into several sub-stories - for full names, ages and positions.  In this example it's simple enough that it makes sense to lump them together, but you always want to make sure that you're not biting off too much at once.

### Interactions

Two other things you'll want to consider during this Details phase are:

* How am I going to store the data?
* How will this system interact with others?  

In this example, the data storage is pretty simple - just a few attributes.  We don't need anything from other systems, but we might anticipate that other systems might need to get a character's demographic information and provide an easy way for them to do so.

I'm a big fan of keeping systems independent of one another's details.  What do I mean?   Well, consider this:  +finger might want to display a character's birthdate.  Do you want it looking specifically at the BIRTHDATE attribute?  What if you decide to change the format of how the birthdate is stored?  What if you move it to a DATE_OF_BIRTH attribute?  Now you've got to change *both* the demographics commands and the +finger commands.  And anywhere else that displays an age.

Instead, you can provide some global functions:  Age(), Birthdate(), Position(), etc.  Now it doesn't matter how the demographics system stores the data -- all the other systems can get the data in an easy, consistent manner.

## Test First

One thing you'll commonly find in professional Agile development is a "test first" mentality.  You might think:  "How silly!  How can I test something when I haven't even written the code yet!?"  In MUSHcode it's very difficult.  The tools are not your friend.

But you can still apply some of the same principles by at least *thinking about* the tests ahead of time.  When you start to think about situations like:   What happens if the player types  +position COWBOY, or +position (space)(space)(space)Cowboy, or +position cowboy .... now you start to think about building handling for that into the code in the first place, rather than trying to bolt it on after the fact.

## Iterate

So, now you've done one story.  Go and do the next, and the next, and the next.  Each time you'll have to revisit some of your old code, adding new functionality and changing some things under the hood.  But you'll be able to see things develop before you know it, and the end result will be pretty cool.