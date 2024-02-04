---
title: Tinkering
description: 
layout: tutorial
quickstartTutorial: true
tutorialName: Code Quickstart
tutorialIndex: tutorials/code/quickstart
nextstep: command-handlers
prevstep: hello-mush
tags:
- code
- code-quickstart
---

The `ruby` command is handy, but often you'll want to run code that's too involved to write comfortably in a single line of text.  For that, we have the `tinker` command.  The `tinker` command lets you enter some code in a mini code editor on the web portal and then execute it in the game.

To change the tinker code:

1. Log into the Web Portal with your coder character.
2. Go to Code -> Tinker.
3. Edit the handle method to do the desired processing (see below for details).
4. Click Save.
5. Back in the MUSH client window, type `tinker` to execute the code.

## Try It!

Let's make the tinker code say hello to us.  Edit the tinker code as described above and make the `handle` method look like this:

    def handle
      client.emit "Hello, #{enactor.name}!"
    end

{% tip %} 
There's other code in the tinker file, but we don't need to mess with that.  In these examples, we'll only be changing the 'handle' method.  The other code will be explained in future tutorials.
{% endtip %}

After saving, go back to your MUSH client (logged in with your coder character) and type `tinker`.  You should see:  "Hello, Headwiz!" (or whatever your character's name is.)

We're going to continue using the tinker command for the remaining exercises in this tutorial.  There's a more in-depth [Tinkering Tutorial](/tutorials/code/tinker.html) if you want to learn more about tinkering when you've finished with the Quickstart.

{% tip %} 
If you get an error when saving or executing your code, check to make sure you've typed it exactly as indicated in each exercise.  Usually errors result from misplaced braces  `{}`  or missing  `end`  statements.
{% endtip %}
