---
layout: page
summary: Historical Info
title: The origins of AresMUSH (2007)
tutorial: true
---

{% note %}
This page is a historical archive of the earliest design vision for AresMUSH. It's fun to see how some things have stayed constant even as others (like SQL) evolved.
{% endnote %}

## Intro

From the player's perspective, AresMUSH will be in the same family as PennMUSH and TinyMUX.  From the game administrator's perspective, it will be something completely different.

## Goals

The goals of AresMUSH are:

1) Provide a modular and extensible MU "engine" using modern technology.

Why?

MUSH servers have evolved (SQL support, softcode formatters, etc.) but for the most part remain entrenched in their '80s roots of heavyweight C/C++ code with a custom pseudo-scripting language.  Hardcode is generally inflexible, and not really intended to be modified.  Softcode is painful to learn and nearly impossible to decipher once written.

2) Reduce the barrier of entry to running a MU with a 'turnkey' installation and easily-customizable core modules.

Why?

It's effectively impossible to set up a MU without a coder, and demand for coders far exceeds supply.  Installation requires compilation of C code.  The basic DB is fairly barren, lacking core functionality that just about every game needs.  Standard code packages like Sandbox Globals, and even my own softcode library are limited in utility and still require a coder to install and configure.

3) Preserve the player experience (within reason) using familiar interfaces and supporting existing clients.

Why?

Even the generally-similar Penn and Tiny servers frustrate players with their subtle differences in commonly-used command syntaxes (mail, channels, etc.).  Radical change will likely spell disaster, but some change is inevitable.


Target "Market"

This project is targeted at new games.  There is probably not much here to compel someone to migrate over an existing game.

 
## Tenets of AresMUSH

What makes AresMUSH different from existing MU servers?

1)  No "softcode"

AresMUSH uses a central 'engine' to handle basic (very basic) functionality.   Everything else – even things that are fairly standard, like poses and movement – is done using 'modules'.  Modules are object-oriented software packages that communicate with the engine and with each other using well-defined interfaces.  Modules can be replaced, modified or disabled so long as their interfaces are respected.  

For example:  TGG might swap out the movement system for one that restricts movement based on action points during combat.  SWS might swap out the description system with one that limits character descriptions based on what clothing items they had purchased.

Modules are implemented in a standard scripting language (probably Python).  This will make the code easier to learn; there are a lot more Python programmers than softcode programmers, as well as books and references on the subject.  Using a "normal" language offers countless advantages over MU softcode – not the least of which are local variables and comments.

Modules are stored server-side and edited as normal text files using an editor of choice.  They can easily be managed using CVS or another version control system.  Modules are loaded at game startup time, and can be reloaded at will during run-time (similar to the way text files are currently reloaded using the @readcache command on PennMUSH). 

Two notable implications of this decision:  Coders will require server access, and regular players will not be able to code utility objects or other random things.  Neither of these things should be a big deal.  If you can't trust your coders, you've got issues, and players shouldn't need utility code if you just give them what they need.   


2)  A standard database

AresMUSH will require a SQL back-end.  Requiring SQL places limitations on the game host (though most support SQL anyway) but opens up a whole host of options with regards to integrating with web pages and other tools, not to mention the efficiencies inherent in using a standard database tool for storing data.

The core engine will maintain a set of base tables.  These tables contain only the minimum data set required for the engine.  Among this data is the "object ID", a unique identifier for each object.  Object IDs are not recycled, even when an object is no longer in use.

Each module maintains its own table(s) with its own data.   What this means is that the data for the skills system is stored completely separate from the data for the description system (in contrast with existing MU servers where most everything is just lumped onto the character object).  


3) Core modules

Although the intention is for modules to be "plug and play" to allow for lots of flexibility, there are a number of modules required for basic gameplay.  These are dubbed the core modules.  Some examples (by no means a complete list):

•	Movement (rooms and exits)
•	Posing
•	Descriptions
•	Permissions/Roles
•	Help
•	Pages
•	Channels
•	Mail
•	Who
•	Finger
•	Etc.

The "core" distinction is somewhat arbitrary.  Core modules are ones that you may want to tweak, but probably never want to disable. Technically you could have a game without a help system, but it's probably not a good idea.  

More importantly, perhaps, the core modules are the ones that will come as part of the base AresMUSH installation package.


4) Skins and Customization

All of the core modules will support customization to some extent, including a central "skin" system.   The details need to be worked out, but the general idea is to enable fast and easy customization of things like room formats, +who appearance, color schemes, etc.  

Likely the system will entail a CSS-like style system coupled with some sort of markup language.  For example, a +who skin might allow you to define three sections for the header, detail of each character, and footer:

    <header>
    <field style=header width=25>$mushname$</field>
    ------------------------------------------------
    </header>
    
    <charDetail>
    <field style=charName width=15>$name$</field><field style=roomName width=20>$location$</field>
    </charDetail>
    
    <footer>
    -------------------------------------------------
    </footer>

The code would know to substitute the configured mush name for $mushname$ and so forth.

(Note: This is just a quick example and the final skin system will probably look nothing like this.)

An open issue is how to store customization and skin info.  Is it in the database or in a set of config files?  Config files might be easier to edit, particularly for multi-line skin files.  The database, on the other hand, is more centralized.

Another idea that needs to be fleshed out is allowing skins to be configurable or selectable by the player.  For instance, possibly allowing each player to pick the colors for their style system, or allowing them to customize which fields they want to see on +who by designing their own skin.


5) Multi-Threaded

Existing MU servers are (I believe) single-threaded.  Periodic actions require the use of @wait, which eventually dumps the next command into the central command queue: 

&annoying-msg object=@wall I'm annoying.;
   @wait 10=@tr me/annoying-msg

Python or a similar language would allow modules to spawn their own threads.  For example:

           AnnoyingThread()  {  
              while(1) { 
                    EmitAll("I'm annoying."); 
                    Sleep(10);}
                }

As with any multi-threaded system, this opens the door for race conditions and coordination issues, but these are not insurmountable.   I expect that in spite of these issues, allowing multiple threads will open new doors and make many things much easier.
