---
title: FS3.3 - Dice Mechanics
description: 
layout: fs3
prev-article: mechanics-overview.html
next-article: combat-mechanics.html
---

For those who care about the nitty-gritty about what the Ability Ratings actually mean in terms of chance of success, this article is for you.

{% include toc.html %}

## Base Mechanic

The basic FS3 mechanic is Attribute + Skill number of 8-sided dice against a target number of 6.

## Chance of Success

On a routine roll, here is the chance of getting various numbers of successes based on the **total** number of dice (attribute + skill).

> <i class="fa fa-cubes" aria-hidden="true"></i>  Tasks in FS3 require only a single success, so even modest skill ratings (Competent or higher) give you a good chance of success on average rolls.  Higher ratings give you more of an edge in opposed rolls and difficult tasks.

| Total Dice (assuming avg. attr.) | 1+ Success | 2+ Success | 3+ Success | 
| ---- |---- |---- |---- |---- |
|3 (Everyman)|76%| 32% | 5% | 
|4 (Fair)|85%| 48% | 15% |
|5 (Competent)|90%| 62% | 28% | 
|6 (Good)|94%| 73% | 40% | 
|7 (Great)|96%| 81% | 52% | 
|8 (Extraordinary)|98%| 86% | 63% | 
|9 (Amazing)|99%| 91% | 72% | 
|10 (Legendary)|99%| 94% | 79% | 

{% include pretty_image.html file='fs3/fs3-multiple-success.png' %}


## Effect of Modifiers

Higher skill ratings insulate you against modifiers, letting you have a good chance of success even when the going gets tough.  Modifiers do not equate to a raw % -- you cannot say that -1 is -10% or anything like that.  The effect of a modifier depends on their original skill, as shown in the chart below.

| Total Dice (assuming avg. attr.)| No Modifier | -1 Modifier | -2 Modifier | -3 Modifier |
| ---- |
|3 (Everyman)|76%|	60%|	37%|	37%|
|4 (Fair)|85%|	76%|	60%|	37%|
|5 (Competent)|90%|	85%|	76%|	60%|
|6 (Good)|94%|	90%|	85%|	76%|
|7 (Great)|96%|	94%|	90%|	85%|
|8 (Extraordinary)|98%|	96%|	94%|	90%|
|9 (Amazing)|99%|	98%|	96%|	94%|
|10 (Legendary)|99%|	99%|	98%|	96%|

Consider Competent Carla (3 skill + 2 attribute) vs. Extraordinary Edward (6 skill + 2 attribute).  If you give both a -3 modifier, Calra's chance just went from 90% to 60%, but Edward's was only reduced from 98% to 90%.  Edward, with his higher skill, is better able to adapt to the challenging circumstances.

{% include pretty_image.html file='fs3/fs3-impact-modifiers.png' %}


## Multiple Successes vs. Modifiers

In FS3, a single success is enough to accomplish a task.  If a task is hard, applying a modifier is better than requiring multiple successes. Here is why it matters.  

Consider Fair Frank (2 skill + 2 attribute) and Good Greta (4 skill + 2 attribute).  The chart below shows their original success chance, compared to the chance of success with a -2 modifier and the chance of success if you require a "Good Success" on the roll (3 successes).

Notice that requiring a "Good Success" makes your chance of success _dramatically_ lower.  Poor Frank has almost no chance at all. In fact, you have to have a total die pool of 7 before you even have a 50/50 chance of getting a 'Good Success' on a roll.

{% include pretty_image.html file='fs3/fs3-modifier-vs-success.png' %}


## Expected Successes

Technically the _possible_ number of successes is always 0 up to the total number of dice.  But in practice, some results are extraordinarily unlikely.  This chart shows you how many successes are actually _practical_.

* Average Successes = Mathematical average number of successes.
* Expected Range = Excluding results that are less than 5% likely, what is the actual range of successes you can expect.

| Total Dice (assuming avg. attr.) | Average Successes | Expected Range |
| ---- |---- |---- |
| 3 (Everyman) |1 | 0-2 |
| 4 (Fair) | 1.5 | 0-3 |
| 5 (Competent) |1.875 | 0-4 |
| 6 (Good) |2.25 | 0-4 |
| 7 (Great) |2.625 | 0-5 |
| 8 (Extraordinary) |3 | 1-5 |
| 9 (Amazing)|3.375 | 1-6 |
| 10 (Legendary)|3.75 | 1-7 |

{% include pretty_image.html file='fs3/fs3-average-success.png' %}

## Modifiers vs Opposed Rolls

Opposed rolls are meant for _active_ challenges, like other characters.  Using opposed rolls, even with low skill levels, can have a far more dramatic impact on your chances of success than even significant modifiers.

{% include pretty_image.html file='fs3/fs3-modifier-vs-opposed.png' %}

## Big Bads / Superhuman Rolls

FS3 does not scale for beyond-human abilities.  Games that want to have superhumans (mutants, jedi, wookiees, etc.) or "big bads" should be aware of this.  Here is a chart that illustrates the problem.

The blue is a regular human rolling 7 dice.   On average he gets between 2-3 successes, but on a lucky roll he might get up to 7.

The red is our Super rolling 20 dice.  On average they get between 7-8 successes, so yes - they will win most of the time.  The regular human can’t even touch their lucky rolls of 10+ successes.

But sometimes the Super rolls that fistful of dice and ends up with only a few successes.  That’s the shaded section in the middle, and that’s where our regular human can win or tie.  It happens more often than you might think.

There's a more in-depth discussion of this in the blog post [Scaling in FS3](https://aresmush.wordpress.com/2019/07/18/scaling-in-fs3/).

{% include pretty_image.html file='fs3/fs3-scaling.png' %}

## Opposed Rolls

When considering the mechanics of opposed rolls, two important things to remember:

1. It's not just win/lose, you can also draw.
2. The more dice you roll, the more "randomized" your results get.

What this means in practice is that opposed rolls don't line up quite as neatly as you might expect.  You'd think 3 vs 3 would have the same breakdown of win/lose/draw as 5 vs 5 because they're all evenly matched, but that's not true.  3 vs 3 has a higher chance of getting a draw than 5 vs 5 because there's more variance in # of successes with 5 dice.

{% include pretty_image.html file='fs3/fs3-opposed-chances.png' %}

{% note %}
These numbers are based on actual roll results over a few thousand samples, not mathematical probabilities.  So you'll see tiny variances like 3 vs 5 is a fraction of a % different than 5 vs 3.
{% endnote %}

### Chance of 'A' Winning or Drawing

||vs|B 1|2|3|4|5|6|7|8|9|10|11|12|
|A||||
|1||80.9|65.4|52.9|43.1|34.6|28.0|21.1|16.8|12.9|10.5|8.1|6.5|
|2||85.0|72.5|61.6|51.4|43.0|35.2|28.2|23.1|19.6|15.3|12.7|9.5|
|3||89.4|78.8|69.4|60.0|50.5|43.2|36.2|30.6|25.3|21.4|17.3|13.6|
|4||92.2|83.3|74.9|66.2|57.2|50.7|42.7|37.8|32.0|26.9|23.3|18.7|
|5||94.1|86.9|79.3|71.9|64.7|57.0|50.1|43.6|37.1|33.2|28.4|24.6|
|6||95.6|89.4|83.5|76.4|69.1|63.6|57.0|50.9|44.6|39.6|34.4|29.7|
|7||96.9|92.7|87.2|80.4|74.6|68.8|61.4|56.7|50.4|45.0|39.2|35.2|
|8||97.4|93.8|89.7|85.0|79.0|73.4|67.6|61.9|56.0|49.6|44.8|41.2|
|9||98.2|95.4|92.0|87.5|82.9|77.7|72.3|65.9|61.3|55.4|49.8|44.1|
|10||98.6|96.4|93.4|89.5|85.1|81.8|75.9|71.1|66.2|60.0|55.2|50.4|
|11||99.1|97.4|94.5|91.7|88.1|83.4|79.6|74.1|69.8|64.9|59.8|55.2|
|12||99.2|97.9|95.9|92.9|90.2|86.9|82.2|78.3|73.6|69.1|64.1|58.9|

### Chance of 'A' Winning


||vs|B 1|2|3|4|5|6|7|8|9|10|11|12|
|A||||
|1||18.4|13.3|10.7|8.6|6.9|6|3.2|2.6|1.2|0.9|1|0.9|
|2||33|26.2|21.5|16.2|13.7|10.6|7|5.9|5.2|3.3|3.1|1.4|
|3||47|38.5|31.7|25.9|19.2|16.8|12.8|10.8|7.8|7.1|4.8|3.6|
|4||57.7|48.4|41.1|33.5|26.1|24|18.1|16.4|11.9|10.1|8.5|6.9|
|5||66.6|57.2|49|41.6|35.6|29.5|25.4|20.5|16.6|14.6|12.3|10.6|
|6||73.4|63.9|57.1|48.4|42.5|36.9|32|27|22.6|20|16.1|13.6|
|7||79.4|71.6|63.5|55.5|49.2|42.6|36.7|33.1|27.6|23.9|20.2|17.7|
|8||82.7|77.1|69.8|63.9|55.3|49.2|43.8|38.2|33.8|28.4|25|23.1|
|9||86.8|80.4|75.3|68.7|61.9|56.5|49.5|43.8|39.3|34.6|30|25.3|
|10||89.3|84.6|78.8|72|66.6|62.4|55.1|50.4|45.1|39.7|34.9|32.2|
|11||92|87.4|81.9|77.2|71.9|65.7|61.3|54.6|50.6|45.1|39.3|35.8|
|12||93.8|89.9|85.8|80.5|74.8|70.8|65.3|59.8|54.6|49.7|45.4|40.3|

### Chance of a Draw

||vs|B 1|2|3|4|5|6|7|8|9|10|11|12|
|A||||
|1||62.5|52.1|42.2|34.5|27.7|22.0|17.9|14.2|11.7|9.6|7.1|5.6|
|2||52.0|46.3|40.1|35.2|29.3|24.6|21.2|17.2|14.4|12.0|9.6|8.1|
|3||42.4|40.3|37.7|34.1|31.3|26.4|23.4|19.8|17.5|14.3|12.5|10.0|
|4||34.5|34.9|33.8|32.7|31.1|26.7|24.6|21.4|20.1|16.8|14.8|11.8|
|5||27.5|29.7|30.3|30.3|29.1|27.5|24.7|23.1|20.5|18.6|16.1|14.0|
|6||22.2|25.5|26.4|28.0|26.6|26.7|25.0|23.9|22.0|19.6|18.3|16.1|
|7||17.5|21.1|23.7|24.9|25.4|26.2|24.7|23.6|22.8|21.1|19.0|17.5|
|8||14.7|16.7|19.9|21.1|23.7|24.2|23.8|23.7|22.2|21.2|19.8|18.1|
|9||11.4|15.0|16.7|18.8|21.0|21.2|22.8|22.1|22.0|20.8|19.8|18.8|
|10||9.3|11.8|14.6|17.5|18.5|19.4|20.8|20.7|21.1|20.3|20.3|18.2|
|11||7.1|10.0|12.6|14.5|16.2|17.7|18.3|19.5|19.2|19.8|20.5|19.4|
|12||5.4|8.0|10.1|12.4|15.4|16.1|16.9|18.5|19.0|19.4|18.7|18.6|


### Chance of 'A' Getting a Solid Victory

||vs|B 1|2|3|4|5|6|7|8|9|10|11|12|
|A||||
|1||0|0|0|0|0|0|0|0|0|0|0|0|
|2||0|0|0|0|0|0|0|0|0|0|0|0|
|3||1.3|0.8|0.7|0.4|0.3|0.3|0.2|0.2|0.1|0.1|0.1|0.0|
|4||3.8|3.2|2.3|1.7|1.3|1.1|0.7|0.6|0.4|0.3|0.3|0.3|
|5||8.5|6.4|4.9|3.9|3.2|2.6|1.8|1.4|0.9|1.1|0.6|0.6|
|6||13.5|10.7|8.9|7.1|6.2|4.5|3.8|3.0|2.2|1.9|1.2|1.1|
|7||19.8|16.0|13.4|11.3|8.9|7.3|5.8|5.1|3.9|3.2|2.7|2.0|
|8||26.6|22.8|18.7|15.6|13.1|10.5|8.7|7.8|5.9|4.4|3.9|3.0|
|9||34.5|29.2|25.6|20.7|16.7|15.8|12.0|10.6|8.9|7.2|5.5|4.7|
|10||41.0|36.0|31.0|26.4|22.4|19.3|16.4|13.9|12.1|8.7|8.4|6.5|
|11||48.8|42.4|37.3|32.8|27.5|23.9|20.4|17.4|14.8|13.2|10.7|8.9|
|12||55.2|49.0|43.2|38.3|33.1|29.3|24.6|21.8|18.3|16.3|14.0|11.8|
