---
title: Web Portal Overview
description: 
layout: page
tags:
- code
- webportal
---

The Web Portal uses a completely different language (Javascript instead of Ruby) and framework (EmberJS) than the game engine/plugins/etc.  That's the bad news.

The good news is that most games won't need to modify the Portal code.  The  Portal offers core functionality that is going to be common across most - if not all - games.  The style is highly configurable without even needing to touch the code at all.

## Ember in a Nutshell

EmberJS is a Javascript web application framework.  It gets its raw data from the game server, but otherwise everything is handled client-side (in the browser).  This allows a more responsive and interactive player experience overall.  It also minimizes load on the server, which is important because MU servers tend to be running on bare-bones hardware.

See [Learning Ember](/tutorials/code/ember.html) for some helpful tutorials on the language itself. 

## Ember Building Blocks

An Ember screen consists of three basic parts:

* A **[Route](/tutorials/code/web-routes.html)**, which gets the data.
* A **[Template](/tutorials/code/web-templates.html)**, which handles the display.
* A **[Controller](/tutorials/code/web-controllers.html)**, which handles any actions resulting from buttons on the screen and helps the template make any decisions about what to show.

In addition, Ember also has some utilities that are used by many screens.

* **[Services](/tutorials/code/web-services.html)** provide centralized functionality - such as the ability to show notices on the screen or talk to the game server.
* **[Mixins](/tutorials/code/web-mixins.html)** are like `includes` in Ruby - they make common utilities available to screens that need them.
* **Helpers** and **Components** are little snippets you can use in other templates.  Helpers are very small - like a utility function call.  Components are self-contained screen widgets.

Finally, the **[Game Api](/tutorials/code/web-game-api.html)** allows the Web Portal to communicate with the game engine.