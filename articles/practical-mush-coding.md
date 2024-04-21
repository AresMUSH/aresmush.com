---
title: Practical MUSH Coding
description: A guide to MUSH Coding intended for mid-level coders.
layout: story
author: Faraday
---

{% note %}
This is a very old article written for PennMUSH, not AresMUSH, and its principles are pretty dated. It is archived here for posterity.  For AresMUSH code tutorials, see the [code](/code) section.
{% endnote %}

When I began coding on Star Wars MUSH in 1993, I was armed with Amberyl's MUSH Manual and a copy of the PennMUSH help files, painstakingly printed out on my dot-matrix printer. I fancied myself a pretty decent coder after a few weeks; I could code a Falcon controller with the best of them, and even tried my hand at a hovercar object. I remember being so proud when I completed my first real project - a little datapad object that let you store, remove, and edit files. But when I stumbled into my first wizard position, on a fledgling MUSH that needed coders, I had the opportunity to work alongside a true "Master Psychocoder". I realized then just how little about MUSH coding I actually knew.

Over the next few years, I slowly began to learn. I place the emphasis on 'slowly' because, much to my dismay, I discovered that there really wasn't a guide anywhere that taught you how to code (at least, not beyond the basics covered in Amberyl's wonderful manual). Fortunately, I had help. A code wiz was there to answer my questions, point out problems in my code, and tell me a few of the tricks and tips that weren't written anywhere. In time, I got the hang of it, and I eventually took up the reins as head coder of Babylon 5 MUSH, a position I held for 2 1/2 years before retiring.

I was lucky to have someone who I could be an "apprentice" to. Someone to show me the path that led from basic coding principles to advanced "psychocoding". Not everyone who wants to learn MUSH coding has the opportunity to work with someone like that, and that's what motivated me to write this guide.

This is not a beginner's coding manual. It assumes that you have some basic knowledge of principles like attributes, dbrefs, user-defined commands, and the like. If you are not comfortable with these principles, I strongly urge you to read Amberyl's MUSH Manual before proceeding with this document. Also, this guide does not delve into things like queue and CPU cycles,  memory usage vs db space, etc. I’ve never had to worry much about that sort of thing, and this is a document about what I have found that works for me. There's a section in Amberyl's manual entitled 'The Art of Psycocoding' if you're interested in that.

What you'll find in this guide is a (hopefully) practical demonstration of what I like to call "journeyman-level psychocoding". It's meant to bridge the gap between a "casual" coder and a true "psychocoder"; to give you enough familiarity with how to do things that you can use these principles in your own coding projects. I hope you find it useful.

{% include toc.html %}

## Reinventing the Wheel

I believe strongly that the only way to learn to code is by doing it. No amount of reading and theory that can substitute for the experience you get by working on even a small code project. Unfortunately, most of the small projects have been done already. +who, +finger, bulletin boards - every MUSH in the world has them. Why reinvent the wheel, if someone's already done the work?

Because that's how you learn. +finger is a fairly trivial task, but it's practice. It reinforces the basic principles used in coding. If you code little things like that often enough, you'll be able to do them in your sleep. Only then will you be able to tackle tasks like a full-blown combat system. Your +finger may not be as fancy as one done by a person who's been coding for 5 years, but it's yours. If you ever want to modify it, or if it ever breaks, you'll know intimately how it works and be better prepared to change or fix it. It's a million times easier to figure out your own code than it is to decipher someone else's.


## Individual Styles

All coders have their own style. They have things they like, things they're comfortable with, and things that they believe work well. Maybe you like @-commands and curly-braces better than functions and square-brackets. Maybe you like to name things DO_mycommand instead of CMD-mycommand.

I make no claims that the methods described in this document are the "right" way. They're simply my way, and they've always worked for me. If you read something here and can come up with a better way of doing the same thing - great! Knock yourself out. This guide is meant to give you one way of doing things. I encourage everyone to experiment with other ways and find what works best for you personally.

## Tiny Portability

This guide is geared towards people using PennMUSH. Many of the functions used here do not exist in TinyMUSH or MUX. However, I believe that the basic principles described here will be useful no matter what version of MU* you're using.

## Examples

Throughout the code in this guide, I try to give concrete examples on how you can use these functions. The db#s are just examples, plucked from thin air. Don’t take them literally.

The key numbers in examples are #100, a test object set WIZARD, #1551 - which should be replaced by your db#, and Faraday, which should be replaced by your name.

In the Try It sections, lines beginning with > indicate what you should type. Items below that show the output based on what you typed.

## Method to the Madness

I work as a software engineer in RL, and I believe it's really important to organize things before you actually start coding. See [[[Large Scale System Design]]] for more information.

## Test It!

Your spiffy new object is all finished, so now its ready to send out to the masses, right? Wrong. You'll never cease to be amazed by the new and interesting and totally **wrong** ways players can use your code. Mistake number one is to assume 'Nobody will ever try that!'. Mistake number two is to allow something really bad to happen if they do.

As much as possible, test all the wacky situations you can think of before unveiling code. If you can, get someone else to test it too. Something that seems obvious to you will baffle others, so get as many second opinions as you can.

Three important things to ALWAYS check for in your code:

### Spaces

Make sure it works if someone leaves a blank space after an equals sign, like: 

    +set me = IC


Here, the trim() function is your friend. trim(%0) and trim(%1) will clear this problem right up.

### Dolists

With attribute-affecting code (code that votes for someone, or increases a stat, or something), make sure it works properly if someone uses an @dolist, like: 

    @dolist 1 2 3 4 5 6 7 8 9 0=+increase_skill me/Unarmed


If there's supposed to be some kind of delay (like you can only increase a skill once per day) or a cost (like increasing a skill costs a certain amount of XP) it's possible that a dolist like this could trigger the beneficial stuff before the delay or cost kicks in. Especially check for this in Chargen code and the like.

### Security

Make sure the function works correctly for both a wiz character and a mortal character. Too often code gets tested only one way. You don't want to give mortals access to your admin commands! Similiarly, it's all well-and-good if the +set command works for WIZ'es - but what about regular folks?

Make sure nothing drastic happens if a sneaky bugger inserts functions into his commands. The MUSH parser is kinda wacky and sometimes will evaluate things you don't want it to. For example, set up a secret attribute on another player, like so: 

    &secret_attribute *Joe=Test 
    @set *joe/test=mortal_dark 
    Then *with a mortal player* try the following: 
    +set me=[pemit(%#,xget(%#,secret_attribute))]IC


If your code isn't secure, this will pemit to your mortal the value of Joe's secret attribute. With other functions, you could do things more drastic than peering at secret values. You could nuke objects, create them, or otherwise mess with them - particularly if you have Function Side Effects enabled. 

Note that these security checks will always work for your Wizard character, even if your code is secure - because you actually have access to the secret_attribute function. That's why you have to test this with a mortal character. 

The biggest risk here is with commands which allow the player to store text which is used by a priveledged (WIZ or ROY) object at a later time. Bulletin boards, News Submissions, Room Descriptions (if the rooms are owned by a master builder)... these are the kinds of things to watch out for. Text stored on the player (like descriptions for a multi-descer or notes for +finger) are usually okay, as is text stored on a player's objects or rooms. 

There are other things to check for, of course, but those are the big ones.

OK, enough with the introduction and disclaimers. Let's get down to the real stuff, shall we?

## Functions

The key to advanced coding is functions. When used in addition to @-commands, they can be a powerful tool indeed. In many cases, they can replace @-commands entirely. There are tons of functions in PennMUSH, but they are different in TinyMUSH and MUX. I'll deal with the PennMUSH variety here.

You can get a list of the standard functions by typing HELP FUNCTION LIST. This will list the categories of functions, and you can get more info on them via the sub-files HELP STRING FUNCTIONS, HELP UTILITY FUNCTIONS, etc. Finally, you can get information on a particular function by typing HELP and then the function name.

Many MU*s have their own global functions which can be viewed by typing @function. You can create utility functions of your own via the same command if you're a wizard.

This next section will give you an introduction to some of the most useful MUSH functions, in order of least complex to most complex (roughly). I encourage everyone to read the help files on these functions to get more information and examples.

Each function contains a description, a usage reference (the syntax of the function) and a series of examples designed for you to try on your MUSH.

### name()

You give it a db#, it gives you the name of that object. This may seem like a trivial function at first, but it's amazingly useful. Many MUSH functions return the db# of something: lcon(), lwho(), loc(), etc. More often than not, humans prefer to deal with names rather than db#s.

%N is a shortcut for the function name(%#)

Usage:

name(db#)

Try it:  
\>think name(#1551)   
Faraday  

\>think name(#100)   
Faraday's Test Object


### num()

This is the name function in reverse. You give it a name, and it gives you the db# of that object. NOTE! You must be in the same room as the object for this to work (this is not true for the name() function). This is particularly important when coding things on a zone object, or an object in the master room (also known as a global object). These objects can only see what's in the room they're in, and not the room you're in.

Usage:

num(db#)

Try it:

\>think num(Faraday)   
\#1551
 
\>think num(Faraday's Test Object)   
\#100

\>think num(Joe)   
I can't see that here.  
\#-1


### pmatch()

This function is a somewhat more useful version of num(). Given a player's name (note this does not work on regular objects, only on players), it will try to find a db# match for that player. You must give it enough of the name to differentiate it from everyone else on the MUSH, but you can use an alias or part of the name.

So if you've got two players, Frank and Fred, you can't just give it pmatch(Fr) because it can't tell which one of them you mean. pmatch(Fra) or pmatch(Fre) would work fine, though. An exception to this is aliases. If Frank has an alias of Fr, then pmatch(Fr) will find him.

pmatch() is exceptionally cool because it will work no matter where on the MUSH the player is. This makes it perfect for global commands. One of its most useful features is that you can give it part of a name, like +finger Fara instead of +finger Faraday, and it will still work.

A useful trick is to use the nested functions: name(pmatch(%0))

This would allow someone, for example, to type +vote Fara, and yet have it store the vote on an attribute VOTES_FOR_FARADAY.

Usage:

pmatch(playername)

Try It:

\>think pmatch(d)  
I'm not sure who you mean.  
\#-2

\>think pmatch(Faraday)  
\#1551

\>think pmatch(Far)   
\#1551

\>think pmatch(gobbledygook)   
No match.  
\#-1


## xget()

This is the basic function to get attributes from an object. It will retrieve the attribute exactly as it's stored, without evaluating anything.

Usage:

xget(db#,attribute)

Try it:

\>&RACE #100=Human  
Faraday's Test Object/RACE - Set.

\> think xget(#100,race)  
Human

\>@alias #100=Nickname  
Faraday's Test Object/ALIAS - Set.

\> think xget(#100,alias)  
Nickname


### u()

The companion to xget(), this function gets an attribute from an object and then evaluates it. Its most common use is to define your own functions. As an optional feature, you can pass parameters to your functions, and reference them as %0, %1, %2, etc. in the function itself.

Usage:

u(db#/attribute)

u(db#/attribute,param0,param1,param2,param3,etc.)

Try It:

\>&TEST_FUN1 #100=These are my notes,%rwhich have linebreaks to demonstrate%rxget() versus u().  
Faraday's Test Object/TEST_FUN1 - Set.

\>think u(#100/test_fun1)   
These are my notes,   
which have linebreaks to demonstrate   
xget() versus u().

\>think xget(#100,test_fun1)   
These are my notes,%rwhich have linebreaks to demonstrate%rxget() versus u().

Note the difference between the output of xget() and u() for the same attribute on an object.

\>&TEST_FUN2 #100=pemit(%0,%1)   
Faraday's Test Object/TEST_FUN2 - Set.

\> think u(#100/test_fun2,%#,This is a test!)   
This is a test!

\>think xget(#100,test_fun2)   
pemit(%0,%1)


### set()

Most people are familiar with the standard way to set an attribute:

    &FOO me=This is foo

set() is just a way to do the same thing with a function. You can set an attribute to the result of another function, or even nested functions. The only trick there is that you have to use square brackets around the function. See the examples below if you're unsure what I mean.

A lesser-used ability of set() is that it can be used to set special flags on attributes. You can use it to set an attribute "mortal_dark". This means that normal players can't see the attribute but wizards and royals can. Useful for hidden attributes like e-mail, skills and profession, etc.

Usage:

set(db#,attribute:value)

set(db#,attribute:[function()])

set(db#/attribute,specialflag)

Try It:

\> think set(#100,race:Human)   
\> ex #100/race   
RACE [#1551]: Human

the number in brackets tells you who set the attribute

\> think set(#100,last_time:[time()])   
\> ex #100/last_time   
LAST_TIME [#1551]: Wed Nov 04 20:41:21 1998

\> think set(#100,faras_name:[name(pmatch(fara))])   
\> ex #100/faras_name   
FARAS_NAME [#1551]: Faraday

\> think set(#100/last_time,mortal_dark)   
\> e #100/last_time   
LAST_TIME [#1551m]: Wed Nov 04 20:41:21 1998

the little 'm' means that it's dark to mortal players


### t()

This is a little function that simply tells you whether something is true or false. Something is false (0) if its 0, #-1, #-2 (or other negative db#s which I've never actually seen used anywhere). Otherwise it's true (1).

Probably the biggest use for this function is in conjunction with the match() function. match(list,item) will return you a position of an item in the list. t(match(list,item)) will be 1 if the item was anywhere in the list, and 0 if it was not in the list.

Usage:

t(expression)

Try It:

\> think t(145)   
1

\> think t(#-1)   
0

\> think t(#1551)   
1

\> think match(Alpha Beta Gamma Delta,Gamma)   
3

\> think t(match(Alpha Beta Gamma Delta,Gamma))   
1


### lwho() / mwho()

This function will list the db#s of all currently connected players if the enactor has permission to see them. That means you or your object has to be ROY, WIZ, or see_all in order to list dark or hidden players when you do lwho().

The sister version of this function is mwho(), which stands for "mortal who". The output of this function is the same as if a "mortal" character had executed lwho(). In other words, it will not list dark or hidden players.

Usage:

lwho()

Try It:

\> think lwho()   
\#1551 #103 #175 #1742

\> think mwho()   
\#103 #175 #1742

assuming Faraday (#1551) is dark or hidden


### loc()

Nifty little function that gives you the location of a player or an object. Note that it returns the location's db#. You can use the name() function to convert this for things like +where commands.

%L is a shortcut for loc(%#) at the time the command is executed

Usage:

loc(db#)

Try It:

\> think loc(#100)   
\#1551

\> think name(loc(#100))   
Faraday

\> think loc(#1551)   
\#1089

\> think %L   
\#1089


### match()

The match() function is used to find the position of a given item in a list. If the item is not in the list, the position is 0.

One if its most common uses is to restrict commands to members of a particular group or faction, if you keep the db#s or names of that faction on an object somewhere.

Usage:

match(list,item)

t(match(list,item)) returns 1 if the item is anywhere in the list

Try It:

\> think match(Alpha Beta Gamma Delta,Delta)   
4

\> think t(match(Alpha Beta Gamma Delta,Delta))   
1

\> think match(Alpha Beta Gamma Delta,Phi)   
0

\> &test_list #100=#1551 #180 #103   
Faraday's Test Object/TEST_LIST - Set.

\> think t(match(xget(#100,test_list),#1551))   
1


### pemit()

This function will send a message to a single player (you can also pemit() to objects but that's rarely useful). Nearly all of your commands will use this, because no matter what the person types - whether it succeeds or fails - you want to give them some clue what just happened.

Some versions of TinyMUX and MUSH do not have this function, which is why I avoid coding on them.

If your MUSH has ansi support, it's often useful to combine this with the ansi() function, which colorizes your messages. The simplest use for this is red for error messages, green for success messages.

Usage:

pemit(space-sep list of db#s,message)

Try it:

\> think pemit(%#,You do this successfully!)  
You do this successfully!

\> think pemit(%#,ansi(hr,This failed!))  
This failed! (it will be highlighted in red if your MUSH has color support)

\> think pemit(%# #1 #2 #3, The time is now [time()])  
The time is now Wed Dec 02 04:34:42 1998 (the message will also be sent to db# 1, 2 and 3)


### emit() / remit()

In the same family as pemit(), these functions are used when you want to send messages to a room. emit() sends to all players and objects in the same room as the emitter (not terribly useful for global objects), and remit() sends to everything in a specific object (usually a room).

Usage:

emit(message)

remit(object,message)

Try It:

\> think emit(The shuttle bay doors open.)   
The shuttle bay doors open. (everyone else in your room sees the same message.)

\> think remit(%L,The shuttle bay doors open.)   
The shuttle bay doors open. (everyone else in your room sees the same message.)

\> think remit(#100,The shuttle bay doors open.)   
You will see nothing. The message is sent to the contents of #100, your test object.


### switch()

If you're familiar with a "real" coding language, you've no doubt used a switch/case statement before. This is simply the MUSH version. If you're not familiar with another language, the easiest way to understand switch() is as an if/then/else statement:

    IF Joe is male THEN say "Joe is a boy"
    ELSE IF Joe is female THEN say "Joe is a girl"
    ELSE (if none of the other cases worked) say "I don't know what Joe is"


Switch() is a very powerful tool, and you will use it often.

Usage:

switch(what to check for,case1,action1,case2,action2,etc...,default action)

for example: (the comments in italics are not part of the code - they're just for illustration purposes)

switch(xget(%#,sex),   
case1>> male,   
action1>> %N is a boy,   
case2>> female,   
action2>> %N is a girl,   
default>> I don't know what %N is

Try It:

\> think switch(xget(%#,sex),boy, %N is a boy, girl,%N is a girl,I don't know what %N is)   
Faraday is a girl


##### Advanced switch()

Now that you've got the basics of switch() down, I'm going to show you one of the most useful tricks I've learned in coding: the true/false switch. It's perfect for error checking things:

    SWITCH 1
    CASE error check 1
    error message 1
    CASE error check 2
    error message 2
    DEFAULT
    what you do if all error checks pass


Usage:

switch ( 1, first expression to check, what to do if it's 1, second expression to check, what to do if it's 1, etc..., what to do if all the expressions were not 1 )

Try It:

\> think switch(1,match(%N,Faraday),Your name is Faraday so you can't use this!,match(%#,#1551),Your db# is #1551 so you can't use this!,You can use this.)   
Your name is Faraday so you can't use this!

If your name was not Faraday and your db# was not #1551, you would see:   
You can use this.


### iter()

The iterate function is vital when working on lists of any kind. It is the function version of @dolist, and can also be thought of as the MUSH version of a FOR loop (sorta). You give it a list, and an action. It performs the action once for every item on the list.

You can use nested functions (notably xget(), or any list function like lcon() and lsearch()) to first get/generate the list, and then act on it. Very useful!

While iterating, the text ## can be used to substitute for the current item. #@ can be used for the number of the current item (i.e. 1 for the first item in the list, 2 for the second, etc).

One important note about iter() is that it automatically puts spaces between items you iterate through. For this reason, if you're going to use %r's to separate items in the list (see the example under Try It for what I mean) then you nearly always want to put the %r at the beginning, not the end.

Usage:

iter ( list, action to perform on the list )

Try It:

note the goofy spacing when the %r is at the end

\> think iter(A B C,#@. ##%r)  
1. A  
 2. B  
 3. C

note the correct spacing when the %r is at the beginning

\> think iter(A B C,%r#@. ##)   
1. A   
2. B   
3. C

\> think iter(Joe Faraday Alphonse,pmatch(##))   
\#147 #1551 #103

\> &test_list #100=#147 #1551 #103   
Faraday's Test Object/TEST_LIST - Set.

\> think iter(xget(#100,test_list),%r#@. [name(##)])   
note that you have to put brackets around functions when you combine them with text or %r's   
1. Joe   
2. Faraday   
3. Alphonse


### setq()

This is a somewhat tricky function, and that's why I've saved it till the end. Its basic purpose is to allow you temporary variable storage in your commands and functions. If you do real code, you do this all the time:

x = 4   
y = 5 + x


You can do the same thing in MUSH code with setq(): 

setq(0,4)   
add(5,%q0)


This is very useful when you want to store the value of something once, and use it repeatedly. But there are a few catches:

The main limitation is that there are only 10 temporary registers, %q0 through %q9. These registers apply once per command - so if your CMD-+FINGER attribute calls FUN_GET_FOO, they both can't use %q0. It's hard to explain, but you'll see an example of how this can be bad in the Try It section.

It is also not a good idea to use setq() on commands that are likely to get executed simultaneously (+where, room parent descriptions), or commands where bad things can happen if setq() gets confused (combat systems especially).

If you really know what you're doing, it's a great tool. But if you're not entirely sure about it (and I fall into that category myself sometimes) then it's safer to avoid this function.

Usage:

setq(register# 0-9, value to place into the register)

from then on, use %q0 through %q9 to reference the value in that register

Try It:

\> think [setq(0,4)][add(5,%q0)]   
9

\> think [setq(0,pmatch(Fara))]Name: [name(%q0)]%rAlias: [xget(%q0,alias)]%rRace: [xget(%q0,race)]   
Name: Faraday   
Alias: Fara   
Race: Human

Here's an example of how setq()s can go awry on you. 

\> &cmd-test #100=$test:[setq(0,5)][pemit(%#,%q0 -- )][u(#100/fun-test,%#)][pemit(%#, -- %q0)]  
Faraday's Test Object/CMD-TEST - Set.

this stores the value of 5 in %q0, pemits that value to you, calls a function, and then pemits the value of %q0 again. You'd think that both pemits would say "5", right? 

\> &fun-test #100=[setq(1,99)]pemit(%0,This is a test, %q1.)   
Faraday's Test Object/FUN-TEST - Set.

\> test  
5 -- This is a test, 99 -- 5

Good - it worked. That's because cmd-test used queue 0, and fun-test used queue 1. But what if we make the function ALSO use queue 0?

\> &fun-test #100=[setq(0,99)]pemit(%0,This is a test, %q0.)  
Faraday's Test Object/FUN-TEST - Set.

\> test  
5 -- This is a test, 99 -- 99

Notice the difference in the ouput. Since both the original command (cmd-test) and the function it calls (fun-test) use register 0, you have a problem. My solution to this has always been to use registers 0-5 in the commands, and 6-9 in the functions they call. Then you never have overlap problems.

## Examples

Knowing what the functions do is one thing, but knowing how to use them is something that comes only from experience. Here are a few practical examples. The actual MUSH code can be viewed through the link at the bottom of the page. For each example, I'll go through the five steps of the coding methodology I mentioned earlier to hopefully show you not only the final product, but also how to make the final product.

### +finger - Getting and displaying data

**What does it do?**

+finger should show IC and OOC information about the character. Specifically, we want it to show their Name, Alias, Race, Status (if they're connected, otherwise it will show when they were last online), Location (if they're not set unfindable), and a general field called Notes which the player can set themselves.

**Where do I get the info I need?**

Let's just go through them one by one:

Name: Use the name() function.

Alias: Aliases are stored on the player's ALIAS attribute. Use xget() to get it.

Race: This will vary from MUSH to MUSH, but usually it's on a RACE attribute. Use xget() to get it.

Status: You'll want to switch() on whether hasflag(db#,connected) comes back 1 or 0. If it's a 1, that means the player is connected, so this should show "Connected and set IC" or whatever IC/OOC/AFK is stored in their STATUS attribute. If it's a 0, that means they're not connected, so this should show "Offline - last connected on Thu Dec 3 10:22:13 1998." Their last connect time is stored on their LAST attribute.

Location: Another switch() for this one, based on hasflag(db#,unfindable). If it's 0, then you can use name(loc(db#)) to get the name of their current location. If it's 1, you just want to say "Unfindable".

Notes: The player sets a NOTES attribute on themselves, and you can use either xget() or u() to evaluate it. If you use xget(), it's safer, but more limiting. The player can't put any executable code in their Notes attribute.

On MUX and TinyMUSH this is particularly vital because you can do really bad things with functions in Notes attributes. On Penn it's not as critical. Since the Notes attribute is getting evaluated on the player, the permissions it has are the permissions of the player. They can't create, destroy, or otherwise mess with anything they wouldn't ordinarily have permission to mess with. Just about the worst they can do is have a random pemit() - annoying, but not dire.

**Processing and formatting:**

The only thing to process, really, is to make sure the player exists before you spam someone with INVALID - No Such Object +finger info. t(pmatch(%0)) will return 1 if there is a player by that name, and 0 if it could not find a match, or if it found too many potential people.

You can be as fancy as you like with formatting. But for example purposes, I'm simply going to use %r's to separate each field, and ansi() to make the titles (Name, Alias, etc) bold and colored.

You probably also want to put a line at the top and bottom of the +finger message to offset it from other text. The easiest way is to use the repeat() function, and repeat a dash or equals sign 78 times (78 is the standard screen width. Always use that in calculations.)

You could also make a custom line (that's what I like to do) which looks cooler and is more personalized. Like ~-~-~-~-~- or something. If you want to do this, make a 78-character-long line and store it on a LINE attribute somewhere. You can use it repeatedly via xget(#100,LINE) and make all your commands use the same style of line.

**Code It**
 
    &LINE Faraday's Test Object=====----====----====----====----====----====----=====----====----====----====-

    &CMD-+FINGER Faraday's Test Object=$+finger *:think [setq(0,pmatch(%0))]switch(t(%q0),0,pemit(%#,ansi(hr,There is no such player!)),pemit(%#,[xget(#1857,line)]%r%r[ansi(h,Name:)][space(5)][name(%q0)] %r[ansi(h,Alias:)][space(4)][xget(%q0,alias)] %r[ansi(h,Race:)][space(5)][xget(%q0,race)] %r[ansi(h,Status:)][space(3)][switch(hasflag(%q0,connected),1,CONNECTED and set [xget(%q0,status)],OFFLINE and last connected at [xget(%#,last)])] %r[ansi(h,Location:)]%b[switch(hasflag(%q0,unfindable),1,UNFINDABLE, name(loc(%q0)))] %r[ansi(h,Notes:)]%r[u(%q0/notes)]%r%r[xget(#1857,line)])


**Test It**

Test it on folks who are connected, folks who are offline, folks who are dark, folks who don't exist, and folks who are unfindable. If you're worried about security, have your mortal PC put some bad things in their NOTES attribute and make sure nothing bad happens. The xget() function (to try and peer at hidden attributes like skills and stuff), set(), and create() functions are good things to check. I believe MUX also has a destroy() function.


### +who - Lists and string formatting

**What does it do?**

This command lists everyone who's currently online, their status (IC/OOC/AFK/etc), alias, idle time, and location.

**Where do I get the info I need?**

The list of db#s for online players can be obtained by mwho() for normal players, and lwho() for staff members. To determine who's who, you can use the orflags() function - to check for WIZ, ROY, or JUD flags depending on your MUSH config, or the t(match()) functions to check if the person is on a STAFF list somewhere.

Once you've got the list of db#s, iter() through them. For each db#, you want to use the same functions as +finger: name(), xget(), and loc(). The idle() function will tell you the number of seconds someone has been idle.

**Processing and formatting:**

There's not any real error-checking to do here. +who doesn't take any arguments, so there's nothing to really mess up.

There is a lot of string processing to do, though. For each field, you need to decide how many columns it gets. Remember to use 78 columns as a screen width. For our example, we'll use the following column widths:

Status - 5 cols, Name - 25 cols, Alias - 10 cols, Idle Time - 8 cols, Location - 30 cols

There are two key functions for formatting columns. mid() will truncate the text so it fits. If your location is 35 characters long, it obviously won't fit in the 30 cols we've given it. So we need to chop it off. ljust() will then "pad" the field with blank spaces on the end so that everything lines up right.

The only other processing comes in for the idle seconds. Tradition has it that idle time will show 10m for 10 minutes, 5h for 5 hours, etc. The function idle(), however, gives you the seconds. The timestring() function will take 301 idle seconds and convert it to 5m 1s. You only want the 5m part, which you can get by using the first() function.

**Code It**

    &CMD-+WHO Faraday's Test Object=$+who:think pemit(%#,[xget(#1857,line)]%rSet%b%bName[space(21)] Alias[space(5)]Idle[space(4)]Location%r [iter(switch(orflags(%#,Wr),1,lwho(),mwho()),%r[ljust(xget(##,status),5)] [ljust(mid(name(##),0,24),25)][ljust(mid(xget(##,alias),0,9),10)] [ljust(first(timestring(idle(##))),8)][ljust(mid(name(loc(##)),0,29),30)])] %r[xget(#1857,line)])


**Test It**

Test with unfindable people, dark people, and people who have been idle for various times. Also test it using a staff member and a mortal.

### +mp (multipage) - commands and attribute manipulation

**What does it do?**

Earlier versions of PennMUSH did not have a convenient way of paging multiple people and letting them know they were all paged with the same message. More recent versions have fixed this, so this example is not so relevant. But it's still a good example of how to combine attribute manipulation and MUSH commands.

With this command, what you can do is type:

+mp Joe Frank=Hey, what do you think about this?

Joe and Frank see: Faraday pages Joe and Frank:Hey, what do you think about this?


Then a little later, type:

+mp Oh, or what about this other thing?

Joe and Frank see: Faraday pages Joe and Frank: Oh, or what about this other thing?

It's the same as page/list but more convenient to type.

**Where do I get the info I need?**

The only info you need, really, is for the second command `(+mp <text>)`, you have to get the list of whoever this person multi-paged last. In MUSH, this is usually available through the LASTPAGED attribute. But as an added feature, we'll store the last multipage in another attribute LAST-MP. Use xget() to get the LAST-MP attribute from the player using the command.

**Processing and Formatting:**

The trick is to "feed" the information from the +mp command to the page/list function and let the MUSH do the work for you.

Unless you want to get really fancy, it's easier to place the two versions of `+mp (+mp <text> and +mp <players>=<text>)` on two separate attributes. The catch here is that +mp * will be triggered if you type +mp blah=blah because it will think "blah=blah" is `%0`.

The only other thing to do is check if the person's LAST-MP attribute is blank. If so, give them an error message. You can do this by using the words() function on that attribute and seeing if it returns 0 or something other than 0.

**Code It**

    &CMD-+MP-SUB Faraday's Test Object=$+mp *:@switch t(match(%0,*=*))=1,,{@switch words(xget(%#,last-mp))=0,think pemit(%#,You have not multi-paged anyone before!),@fo %#={page/list [xget(%#,last-mp)]={\%0}}}

    &CMD-+MP-INITIAL Faraday's Test Object=$+mp *=*:@fo %#={page/list %0={\%1}};think set(%#,last-mp:%0)


**Test It**

Try using +mp <text> when you haven't paged anyone before, and see if you get the error. Then try pages with text and poses to various combinations of people. Use both the full version +mp <names>=<text>, and the short version +mp <text>


### +check - Putting it all together

**What does it do?**

We'll assume that skills are rated from 1-100, and the success of a "skill check" is determined by a simple percentage roll. If the percent roll is less than the skill level, it succeeds. If not, it fails. This is an incredibly simplistic view of a skills system, but hey - it's just an example.

**Where do I get the info I need?**

Your skills should be stored on a SKILLS attribute, like:

    &SKILLS me=Brawling:60 Swimming:45 Medicine:30

You can get someone's skill rating by iter()-ating through their skills and seeing if one of the skills matches. If it does, use after(##,:) to get the number. You can also use the grab() function but that's too easy, so I'll leave the iter() example in here.

To get the random percentage, use rand(101) - you need 101 to generate a number between 0 and 100.

**Processing and formatting:**

There are two things to error check: a) does the person have the skill, and b) does the skill exist

The master skill list should be stored on a SKILLS_LIST attribute on an object somewhere, like:

    &SKILLS_LIST #100=BRAWLING SWIMMING MEDICINE ART MUSIC

You can see if a skill exists by using t(match()) on the skills list. If that returns 0, the skill is invalid and an error message should be sent to the user. Similarly, use t(match()) on the character's skills to see if they have it. If they don't, show them an error message.

Lastly, you obviously need to compare the percentage rolled to the random number generated, and remit() a message to the room saying whether the skill check succeeded or failed.

**Code It**

    &SKILLS_LIST Faraday's Test Object=BRAWLING SWIMMING MEDICINE ART MUSIC

    &CMD-+CHECK Faraday's Test Object=$+check *:think switch(0,t(match(xget(#1857,skills_list),%0)),pemit(%#,ansi(hr,That is not a valid skill!)),t(match(xget(%#,skills),%0:*)),pemit(%#,ansi(hr,You do not know that skill!)),remit(%l,ansi(hg,%N checks %0 and [switch(lt(rand(101),iter(xget(%#,skills),switch(t(match(##,%0:*)),1, after(##,:)))),1,is successful.,fails.)])))

**Test It**

Try skills that don't exist, and skills that you don't have. Also try it a number of times with differing skill levels so you can see if the percentage comparison seems to be working reasonably.

## General Tips

A few misc. tips and comments to wrap things up.

### Consistency

One important thing in MUSH code is to keep things consistent. It gives an air of organization to the code, and makes things easier to remember - both for you and the players.

If you like to use +command <option1>/<option2>/<option3> then don't all of a sudden change and make one command like: +command <option1>=<option2>=<option3> unless you have a special reason to do so.

By the same token, it looks nice if you use your own custom line instead of simply repeating dashes across the screen.

Lastly, be consistent in how you name attributes. Tradition is to name all $-commands something like CMD-foo or DO_foo. Functions are typically F_foo or FUN-foo. Use whatever convention you like - just do it consistently.

## Colors

Colors may seem like a trivial thing to worry about, but the use of color in your MUSH code can make it look so much cooler. Don't go wild with colors - I've seen places that are just outright gaudy, where the colors are more distracting than useful.

Colors can also be useful because they make people take notice. Highlighting key parts of descriptions, warnings, or error messages can draw people's attention to important details, in addition to spicing up the way things appear.

When using color, be careful to consider potential display color schemes used by your players. Most players tend for either a white-on-black or black-on-white display scheme. To accommodate both display modes, it is advisable to steer clear of using white or black text. Even some of the very light colors (yellow or cyan) can be difficult to read on a white background.

Also avoid overusing the blink/flash tag. Most players find this extremely annoying, so I recommend reserving it only for extremely urgent warning messages.

## Objects in Master Room

One thing to be careful of is placing objects in the master room (usually #2 on most MUSHes). Whenever anybody types a command, every attribute on every object in the master room (and every parent of every object in the master room) is checked for a match.

On most modern machines, this is not an issue.  But it's still unnecessary to put data objects in the master room.

### Planning and Design

I can't stress enough the importance of plotting things out ahead of time. You should never begin coding a major system until you have a firm idea of what it's going to do and how it's going to work.

### Usefulness and RP

Every piece of code on the MUSH should be evaluated for its usefulness before it goes into "production", and you should review your commands periodically to see if any of them have fallen into disuse or have become out of date.

One last comment, which is perhaps the most important one of all: The main purpose of MUSH code is to enhance Roleplay on the MUSH. Never to replace it, and never to simply prove that "yeah, I can code the most sophisticated <insert name> system in existance".  Just because you **can** code something doesn't mean that you **should**.