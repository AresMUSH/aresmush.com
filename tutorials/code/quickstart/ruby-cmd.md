---
title: Ruby Command
description: 
layout: tutorial
quickstartTutorial: true
tutorialName: Code Quickstart
tutorialIndex: tutorials/code/quickstart
prevstep: apis
nextstep: next-steps
tags:
- code
- code-quickstart
- api
---

Throughout these tutorials, we've been using the `tinker` command. There's another way to execute code on-the-fly in Ares, and that's the `ruby` command. This lets you execute single-line ruby code snippets from the MU client. You can't do error checking or complex logic in the ruby command, but it's handy for quick tasks.

## Try It!

Type this into your MU client:

    ruby "Your name is #{enactor.name}"

## Notes

A couple notes:

* The ruby command gives you access to `enactor` the same way the tinker command does.
* Ruby automatically emits the results of the command back to you, so you don't need to add a `client.emit` the way you did in the tinker commands.
* If your ruby code doesn't result in a string to emit, you might see garbage back. 


For example:

    ruby Character.named("Faraday")
    
Will output something like:

    #<AresMUSH::Character:0x00007fa373c81e78>
    
This is because you can't emit an entire character object.

This would work just fine though, because 'name' is a string:

    ruby Character.named("Faraday").name
