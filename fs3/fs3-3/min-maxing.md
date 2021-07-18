---
title: FS3.3 - Managing Min-Maxing
description: 
layout: fs3
prev-article: tweaking-fs3.html
---

One of the common complaints with FS3 is that it encourages min-maxing because it has linear chargen costs and exponential XP costs.  This article addresses why it is this way and what you can do to ensure that it doesn't get taken to extremes.

{% include toc.html %}

## Why is FS3 This Way?

I've studied RPG systems for decades, and FS3 embodies elements from my favorite systems.  Two things that my favorite systems have in common:

**They don't punish you for being good.** I don't want to play the teenage adventurer just starting out in life, or the one-dimensional ace fighter jock.  I want a system that lets me play someone who's good *and* decently well-rounded.

**They have a quick and easy chargen.**  Nothing aggravates me more than having to shift points around like:  "Well, if I just shave this rating 5 to a 4, I'll have 3 more points that I can put over here..."  It makes me want to pull my hair out.  I just want to run down a list of skills and pick levels that fit my vision for my character.

> <i class="fa fa-key" aria-hidden="true"></i> **Key Point:** These two design goals naturally lead you to a system with a 1-1 point/rating cost in chargen, with no penalty for having some skills at high ratings.

Of course you *could* do it differently.  Any number of systems do, by having tiered skill costs, or skill costs tied to attribute ratings, or whatever.  But each of those systems runs contrary to the two goals stated above.

Why not make XP also 1-1 to make it "fair"?  Slow XP gain combats the MU "dino effect" where veterans end up way ahead of new characters.  Also, if you allow people to start out awesome *and* advance quickly, they'll rapidly achieve untouchable levels.

## Why Do People Think This is a Problem?

When you have a 1-1 point/rating and exponential XP cost, you see behaviors like:

* "I may as well max out my Firearms since it's cheap and I'm going to be using it all the time."
* "Eh, I can get by without Persuasion to get another dot in Firearms; I'll buy it later."
* "Wow... I better max out Firearms because it's going to be too expensive to raise with XP."

This min-maxing is a natural and forseeable consequence of the system, so what's the big deal?

Consider two characers:  Bob and Mary.

Bob plays the min-max game and starts with Firearms:6, Melee:5 and 4 points in lower-rated secondary skills.  He doesn't bother putting points into anything he thinks he can get by without.

Mary tries to make up a more balanced and realistic character, starting with:  Firearms: 4, Melee: 3 and 8 points in secondary skills.

Fast-forward six months.  Mary has been pumping XP into Firearms and Melee, but her ratings haven't budged yet because advancement at the higher levels is slow.  Meanwhile, Bob has picked up a few extra secondary skills.  Now it looks like:

* Mary still has Firearms: 4, Melee: 3 and 8 ponts in secondary skills.
* Bob has Firearms: 6, Melee: 5 and now *also has* 8 points in secondary skills.

**Some people think this is terrible.**  They think that Mary is being "punished" for trying to make a more balanced character.  They think that it's hideously unfair that Bob has such an advantage over Mary.

## Method to the Madness

The first thing to realize here is that the Bob/Mary example is working exactly as designed.  "Wait, what?"  It's true.

If FS3 were a level-based game, the admin of the Bob/Mary example basically allowed Bob to start off at level 5 while Mary was still back at level 2.  It doesn't matter how Bob and Mary spend their XP.  If they're earning XP at the same rate **Mary will never catch up to Bob** because she started behind him from the get-go.

> <i class="fa fa-key" aria-hidden="true"></i> **Key Point:** FS3 does not strive for power balance between characters.  Some may be more "powerful" than others depending on how they spent their points.

Why does FS3 allow unbalanced characters?  It is intended for **co-operative PVE games**.  It's a system that allows the grizzled combat veteran to co-exist with the fresh-faced yet talented new recruit -- a cook alongside a figher pilot.  Everyone has equal **opportunity** to make a powerful character.  Whether or not they do, though, is up to them.

FS3 relies on game admins to keep players from going to extremes and making up stupid, one-dimensional, maxxed-to-the-gills caricatures.

So how can you, as a game admin or as app staff, enforce balance?

## Setting Limits

You can choose how powerful you allow characters to be.  You can force them to be well-rounded by *making* them take points in secondary action skills and background skills.  You can set a total point cap, to prevent somebody from being good at everything no matter how many XP they eventually accumulate.  

By adjusting these limits, you effectively limit how much min-maxing is even possible. Bob might *start out* with an advantage over Mary, but he can't continue growing forever.  He'll reach the cap sooner, and Mary will eventually catch up.

Here are a few examples of the available limits built into the AresMUSH FS3 code.  For more information, see [Configuring FS3 Chargen](/tutorials/config/fs3skills_chargen.html) and [Configuring FS3 XP](/tutorials/config/fs3skills_xp.html).

* **Total Attributes / Action Points** - Setting a maximum number of attributes / action points keeps characters from being good at everything.
* **Ability Limits** - Cap the maximum starting ratings and give them room to grow.
* **Max High Skills** - Limit how many abilities can be taken at higher ratings.
* **Skill Minimums** - Set up minimum skill ratings for different groups (positions/factions).  For example: BSGU used this to set up the skills that were taught in basic training and physical qualifications, requiring pilots to at least spend a couple points in firearms and athletics.
* **Minimum Background Skills** - Enforce a minimum number of points spent in background skills, requiring characters to be at least a little bit rounded.

## Make Secondary Skills Useful

Another way to minimize min-maxing is to make sure your secondary Action Skills are actually useful.  Don't bother having Drive or Swimming or Persuasion if you're not actually going to let people use them in meaningful ways.  Save those things for background skills.  

Having useless Action Skills is a sure-fire way for people to skimp on them in order to buy things they think are actually going to come up.  And it really does penalize people who take Drive and never get to use it.  Don't do it!

## Don't Allow Characters to Be Overshadowed

One common complaint about disparate power levels is that the generalists feel overshadowed in plots.  "Why even bother showing up if Bob can do everything I can do, only better."   There are a number of ways you can combat this issue.

* **Balance Conflicts** - Make sure that your conflicts are balanced so nobody feels useless.  This is sometimes hard, since you're at the mercy of the dice, but if there are newbies along for the ride make sure there are some softball targets for them.
* **Maintain Niches** - Just because somebody *can* +learn Demolitions or Medicine doesn't mean that they *should*.  Is their character reallly going to take a bomb disposal course or go to paramedic school?  By limiting who can purchase or learn certain skills at higher levels, you can maintain niches and help characters feel useful.

## Set Expectations

FS3 is not set up for the traditional Hero's Journey.  If you have someone coming into the game expecting that, they're probably going to get frustrated and disappointed.  It's better to set clear expectations from the start.

And it's okay to be flexible.  If somebody messed up their points in chargen and realizes they've hamstrung themselves?  Let them fix it (within reason).  If someone's doing something special, like an intensive 8-week crash course in Viper training?  It's okay to give them some bonus skill ratings outside of what the XP system says.  

Always remember - the system is there to help you tell stories, not to stand in your way.