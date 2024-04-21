---
title: Scaling in FS3
date: '2019-07-18'
layout: post
description:
categories:
tags: [feature, fs3]
author: Faraday
preview_image: soldier.jpg
teaser: The trouble with Big Bads in FS3.
---

I’ve often said that FS3 does not scale well for beyond-human abilities. But why is that? This blog post gives some detailed examples to help you understand the limitations of the dice mechanics.

We’ll start with a tale of two soldiers – Cate and Charlie. Cate’s a pretty good marksman (Firearms: Good, Reflexes: Good = 7 dice), but Charlie’s an expert sniper (Firearms: Amazing, Reflexes: Exceptional = 11 dice).

Let’s take them to the shooting range. Shooting a stationary bullseye at modest distance isn’t so hard, so there are no special dice modifiers.  Let’s say they each get 5 shots per round to score points by hitting the bullseye.  Whoever gets more points wins the round.  How’d they do over 1000 rounds?

{% include pretty_image.html file='postpics/charlie-vs-cate2.png' %}
 

Charlie wins most of the time, as we’d expect, but Cate still wins almost 1 in 10 rounds, and ties about another 25% of the time.

One could legitimately argue that this is silly, and Charlie should win more often.  I can accept that argument, but FS3 works this way **for a reason**, to keep players on a more even playing field.  People with high skills absolutely do better on average, but they don’t leave everyone else eating their dust.

Now what happens if we give Charlie some kind of “power” that gives her +3 dice (total of 14).  We’d expect her to do much better, right?

{% include pretty_image.html file='postpics/charlie-vs-cate3.png' %}

Well, she does, but Cate still ties or wins about 10% of the time.  That seems a little strange against someone with super powers, doesn’t it?

Now let’s give Charlie insane superpowers.  Like “Captain America” reflexes.  20 dice vs Cate’s 7.

{% include pretty_image.html file='postpics/charlie-vs-cate4.png' %}

Of course now Charlie almost always wins, but there’s still that sliver of just under 5% where Cate can beat her to a stalemate.  Does that make **any** sense at all for a slightly-above-average human soldier going up against Captain America?

No.  It’s stupid.

## Looking at the Dice

So why are FS3 dice like this?   Actually any system that uses a “roll + count successes” mechanic suffers from the same basic phenomenon.  Anyone who’s thrown an entire fistful of d6’s in Shadowrun and come up with only 1 success has experienced this first-hand.  It happens with reasonable frequency.

The chart below illustrates this.  I did 1000 rolls and counted how many successes Cate and “Super-Charlie” got on each roll.

{% include pretty_image.html file='postpics/success-overlap.png' %}

The blue part of the graph shows Cate’s successes (rolling 7 dice).  On average she gets between 2-3 successes, but on a lucky roll she might get up to 7.

The red part of the graph shows Super-Charlie’s successes (rolling 20 dice).  On average she gets between 7-8 successes, which is why she wins most of the time.  Cate can’t even touch her lucky rolls of 13+ successes.

But sometimes even Super-Charlie rolls that fistful of dice and ends up with only a few successes.  That’s the shaded section in the middle, and that’s where Cate can win or tie.

It doesn’t happen all the time, but it’s often enough to be noticeable.  Especially on MUSHes where the average number of “rolls per session” is low.  Aberrant results stick out like a sore thumb and stay in peoples’ memory.

## But What About WoD?

Some might wonder why WoD doesn’t have this same problem, since it uses the same basic “roll + count successes” mechanic, with super powers added on top of skill+attribute.

Well, I think it does have the issue, to an extent.   But the skill ranges, dice type and success target number in FS3 magnify the effects.  FS3 is deliberately skewed towards success at the lower levels, and that creates a plateau at the higher levels that you don’t hit in WoD until you start getting really high.  Also, the effects aren’t quite as jarring when you have super-on-super action, as is typical in WoD.

## Difficulty Factors

You might ask yourself–why bother getting high skills, if it doesn’t make you an unstoppable badass?  Difficulty, that’s why.

Let’s take Cate and Charlie (the regular version, not the super-powered one) out to the range again.  Only this time, the targets are moving (difficulty -1) and at longer distance (difficulty -1) and it’s raining (difficulty -1), oh and an automated machinegun turret is shooting over their heads creating a suppressive fire effect (difficulty -1).   Now how do they match up?

{% include pretty_image.html file='postpics/difficulty.png' %}


See the difference? Instead of winning ~70% of the time, Charlie now wins 91% of the time.  Cate never wins, and only draws occasionally.

Higher skill ratings in FS3 insulate you against difficulty modifiers.  They help you succeed when the chips are down.  They let you make that impossible Hero Shot.  So they do matter; they just don’t let you wipe the floor with everyone else in a routine competition.

## Other Considerations

There are other factors in the combat system specifically that make FS3 unsuitable for beyond-human abilities, but that would be even harder to explain.  If folks are really curious, I can dive into that in a separate article, but I think that’s enough math for today 🙂

Incidentally, the Cate/Charlie example was inspired by an actual marksmanship contest on BSG:U where Cate improbably beat out Charlie for the title.  Dice are weird, but fortunately everyone was a good sport about it.

> All the graphs/results in this blog post are actual results from 1000 simulated trials in real FS3 code.  They are not statistical models.  My stats fu is rusty 🙂