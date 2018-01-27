---
toc: ~config~ Configuring FS3 Combat
title: Configuring FS3 Combat vehicles.
---
# Configuring FS3 Combat - Vehicles

To configure the FS3 Vehicle List:

1. Go to the Web Portal's Admin screen.
2. Select 'Advanced Configuration'.
3. Edit `fs3combat_vehicles.yml`

## Vehicle Types

You can specify as many different kinds of vehicles as you like.  They each have a number of statistics, explained below:

    Viper:
        description: "Viper space fighter"
        pilot_skill: Piloting
        toughness: 0
        hitloc_chart: Fighter
        armor: Viper
        weapons:
            - Kew
        dodge: 1

### pilot_skill

Pilot skill is used as the defense skill when someone targets the vehicle.

### toughness

A vehicle's toughness gives it a bonus (or penalty, if negative) to the pilot's knockout roll when the vehicle takes damage.

> **Tip:** Even a +/-1 can make an impact.  You probably don't want to go beyond +/-3.

### armor

You must specify what armor type (see [Configuring Armor](/tutorials/config/fs3combat_armor)) applies to this vehicle.  Vehicle armor is automatic; you don't use the `combat/armor` command to set it.

### hitloc_chart

You also need to specify what hit location chart (see [Configuring Hit Locations](/tutorials/config/fs3combat_hitloc)) applies when the vehicle takes damage.

### weapons

You can specify what weapons are available on the vehicle.  The first one in the list will be the one selected for pilots/passengers by default.

> **Tip:** If a vehicle has multiple configurations (for instance - a BSG Raptor that could have either an air-to-air or air-to-ground loadout) you can either list all weapons and handle it through RP, or break them into separate vehicle types.

### dodge

Nimble or lumbering vehicles may have a bonus (or penalty, if negative) to the pilot's defense roll.

> **Tip:** Even a +/-1 can make an impact.  You probably don't want to go beyond +/-3.