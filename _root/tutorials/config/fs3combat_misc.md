---
toc: ~config~ Configuring FS3 Combat
title: Configuring miscellaneous FS3 Combat options.
---
# Configuring FS3 Combat - Miscellaneous

This topic describes some miscellaneous combat options you can configure.

1. Go to the Web Portal's Admin screen.
2. Select 'Advanced Configuration'.
3. Edit `fs3combat_misc.yml` 

## combatant_types

Combatant types in FS3 let you specify different kinds of soldiers, pilots, aliens, etc.  Each combatant type can have a different weapon, skills and armor.  

> **Note:** The "Observer" type is special and cannot be changed.  The rest can be configured as you desire.  

For example, this BSG config sets up a Soldier type for ground marines and a Viper type for a viper pilot.  The soldier starts with a rifle and armor, and the pilot starts off piloting a Viper.

        Soldier:
            weapon: Rifle
            weapon_specials: 
                - Ap
            armor: Tactical
            hitloc: Humanoid
            defense_skill: Reflexes
        Viper:
            vehicle: Viper
            hitloc: Humanoid
            defense_skill: Piloting

### hitloc

(**Required**)  This controls which hit location table (from [Hit Location Config](/tutorials/config/fs3combat_hitloc)) is used for this type.

> **Note:** For combatants with vehicles, hit location is for the pilot, not the vehicle.  Vehicles automatically have their own hit location table.

### defense_skill

You may override what defense skill this combatant type uses.  If not specified, the system will default to the `default_defense_skill` specified in the [Combat Skills Config](/tutorials/config/fs3combat_skills).

### weapon and weapon_specials

You may give the combatant a weapon and weapon specials.

> **Note:** For combatants with vehicles, they will select the vehicle's default weapon if you don't specify a combatant weapon.

### armor

You may give the combatant armor.

> **Note:** For combatants with vehicles, armor is for the pilot, not the vehicle.  Vehicles automatically have their own hit armor.

### vehicle

You may specify a vehicle type that the combatant will use.


## default_type

You need to specify which of your combatant types is the default if the player doesn't specify a value.  Just set the `default_type` value to one of the combatant types (e.g. Soldier).

## stances

You can configure what stances are available in combat and the attack/defense modifiers they convey.  

> **Important:** If you change/remove the names of any of the built-in stances, you'll want to check the code too.  Some of the stances have special effects (notably Cover and Hidden) in addition to the stance modifiers.