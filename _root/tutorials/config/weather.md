---
toc: ~config~ Configuring the Plugins
title: Configuring the weather system.
---
# Configuring the Weather System

To configure the Weather plugin:

1. Go to the Web Portal's Admin screen.  
2. Select Advanced Config.
3. Edit `weather.yml`

## How Weather Works

Ares has a fairly simplistic weather system.  You can define **climates** with different weather patterns available by **season**.  Each weather pattern consists of a **temperature** and a **condition**.

For example:

        temperate:
            summer:
                temperature: hot hot hot hot hot warm warm warm cool cool
                condition:  clear clear clear fair fair fair drizzling drizzling overcast raining
                stability: 70
            spring:
                temperature: cool cool cool cool cool warm warm warm warm warm
                condition:  clear clear clear fair fair fair drizzling drizzling overcast raining
                stability: 70

Every time the weather cron job runs, there's a chance the weather will change.  That chance is determined by the **stability** of the weather.  If the stability is 70, that means there's a 30% chance of the weather changing.  In other words, the weather will shift roughly once every 8 hours.

When the weather does change, the system will select a random temperature and condition from the seasonal list.  By default, there are 10 entries in the list, meaning each entry has a 10% chance of occurring.  You can make some entries more likely than others by repeating them multiple times.  In the spring example above, there's a 30% chance of clear skies, 30% chance of fair weather, 20% chance of drizzling, 10% overcast, 10% raining.

> **Tip:** You are not limited to ten entries.  That's just convenient for understanding that each entry represents a 10% chance.  You could have 20 entries (5% chance each) or even 100 entries (1% chance each) to fine-tune the weather as much as you want.

Seasons follow the RL northern hemisphere dates based on the IC time.  In other words, January would be winter and July summer.  If you want to make this more sophisticated (like accounting for different seasons on different planets, or months like November which are half winter and half fall), you'll have to change the code.

## climate_for_area and default_climate

The weather system lets you configure a climate for each room **area**.  For all areas that are not specified, the weather system will use the `default_climate`.  You can use 'none' to disable the weather system for that area.

For example, the following config will use the polar climate for the North area and disable weather in the offstage area.  Any other areas will use the temperate climate.

    climate_for_area:
        Offstage: none
        North: polar
        
    default_climate: temperate

To disable weather completely, you can just make the default_climate 'none'.

## temperatures and conditions

These lists control what temperatures and weather conditions are available for your use.  If you want temperatures and conditions beyond the default ones, you'll have to change the code - specifically, the weather translations file.

Each weather condition has a locale entry like so:

    en:
        weather:
            clear: "The skies are clear."
            fair: "The weather is fair."

Also, each combination of season, temperature and weather must have a locale entry like so:

    en:
        weather:
            hot_spring_morning: It is a hot spring morning.
            hot_spring_day: It is a hot spring day.

For more information on how locale files work, see the [Locales Tutorial](http://aresmush.com/tutorials/locale) on aresmush.com.

## weather_cron

The game will periodically change the weather.  There is a cron job to control when this happens.  By default it does this every hour.  See the [Cron Job Tutorial](http://www.aresmush.com/tutorials/code/configuring-cron) for help if you want to change this or turn it off.
