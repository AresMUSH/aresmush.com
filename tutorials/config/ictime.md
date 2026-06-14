---
title: Configuring the IC Time System
layout: page
tags:
- config
---

The IC Time plugin lets you track an IC date/time that's different from the OOC time.  

To configure the IC Time plugin:

1. Select Admin -> Setup.
2. Edit `ictime.yml`

{% include toc.html %}

## How It Works

Because this system uses built-in Ruby date libraries, there are some limitations.  It assumes that your IC calendar mirrors RL's: 7 days a week, 365 days a year (except on leap years), 12 months a year with the same lengths (month 1 -> 31 days, month 2 -> 28 days, etc.).  

You can:

* Adjust the year, so June 1, 2017 becomes June 1, 1817.
* Shift the day, so June 2017 becomes December 1817.
* Adjust the time ratio, so if 1 month passes in RL, 2 months pass IC, or 1/2 month passes IC.
* Change the names of the days and months.

These conversions may occasionally give you odd results.  For example - if today is 2/29/2016 (a leap year) and your date offset is 10 years - there's a problem because 2/29/2026 is NOT a leap year.  That date is invalid, so the game will jump to 3/1/2026 and stay there until March 2nd.  So you end up with a really long March 1st ICly.

If you need a more robust IC calendar, you'll need to write custom code.  But for a quick-and-dirty system, this one should fit the needs of many games.

## year_offset

You can shift IC time by a number of years compared to RL.

For example, assume it's currently 2017 in RL.  To make it 1817 you would set the `year_offset` to -200.  June 1, 2017 would then become June 1, 1817.

    year_offset: -200
    day_offset: 0

## day_offset

You can also shift the game to be a number of days ahead of or behind RL.  You might want to do this if you had a particular starting date in mind (like you wanted to start a WWII game on D-Day even though it wasn't June in RL).

For example, if it's June 1, 2017 and you want the date to be 200 years and 6 months ahead of RL, you can do:

    year_offset: 200
    day_offset: 180

June 1, 2017 would then become roughly Dec 1, 2217. 

{% tip %} 
The exact day it shifts ahead to will vary due to months having different lengths.  Just keep adjusting the day offset until you get the starting date you want.  From there it will advance normally as time passes.
{% endtip %}

## month_names and day_names

The IC date defaults to using the game's locale language for its month and day names.  If your game uses a different calendar, you can change the month and day names.  The system uses a 7-day week and 12-month year, same as RL.

For example, my old Mars game used Latin-inspired days of the week for timekeeping in the Mars colonies, so the `day_names` config would have been:

    - Sol Solis
    - Sol Lunae
    - Sol Ares
    etc.

## time_ratio and game_start_date

The default time ratio is 1, meaning that IC time passes at a 1:1 ratio compared to RL time.  For every day that passes in the real world, a day passes in the game world.  

You can change this ratio to make IC time pass slower or faster.  

* To make time pass faster, set the ratio greater than 1.  Making the ratio 2 would mean that 2 IC days pass for every 1 day in RL.
* To make time pass slower, set the ratio less than 1.  Making the ratio 0.33 would mean that 1 IC day passes for every **3** days in RL.

To make this work, you also need to set `game_start_date`, which is the RL date that the clock starts running.  This should be a RL date in mm/dd/yyyy format.

For example:  Assume your game started on 6/1/2018.  It is now June 10th 2018 in RL, meaning 10 days have passed since the game started.  If your time ratio was 2, the IC date would be June 20th.  If your time ratio was 0.5, the IC date would be June 5th.




