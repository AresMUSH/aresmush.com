---
title: Direct Editing (Transcript)
description: 
layout: tutorial
editCodeTutorial: true
tutorialName: Editing Code
tutorialIndex: tutorials/code/edit-code
nextstep: ftp-upload
tags:
- code
---

This is the transcript for the [Directly Editing Code](/tutorials/code/edit-code/direct-edit.html)  segment of the Editing Ares Code tutorial.

## Introduction

Hi.  This is Faraday from AresMUSH and in this tutorial I’m going to show you how to edit the code directly on your Ares game server.  And we'll talk about why this is the simplest - but not necessarily the best - way to edit your code.

## Connecting to the Server Shell

Let’s assume we’ve followed the installation instructions and have our own Ares game running somewhere in the cloud.

To connect to the game, we need to use SSH - which is basically the secure version of telnet.  There are a variety of ways to do this.  The easiest way is to download an SSH client application, such as PuTTY - which is one of the more popular ones that runs on both Windows and Mac.  On a DigitalOcean droplet, you can connect from the droplet management page.  You can also connect using the Mac terminal or Windows powershell.

However we got there, we can navigate around the server shell by typing commands.  ls lists the files.  cd changes directories.  Most of the code we’re going to edit lives in the aresmush/plugins directory, where there are folders for each plugin.

## Editing Files

In this example, we’re going to edit the tinker command.  Now if you’ve done the first coding tutorial on aresmush.com, you know that we can edit this command through the web portal.  Here we’re using it as an example to show how you could do the same thing through the server shell.  You can use the server shell to edit any command - not just the tinker command.

In order to edit the tinker command file, we need a command line editor that will run in this terminal shell.  There are several available.  The one I like to use is nano - and you just type nano and the filename.  

There’s our code.  Here’s the command handler, and we can change it to do something different - like emitting Hello World.

To save it, it’s CTRL-O, and the commands are helpfully there at the bottom for easy reference.

## Loading Changes

So now our file is saved.  If we go back over to the game and type ‘tinker’, we might expect to see our “hello world”, but we don’t.

Why is that?    In Ares code, it’s important to remember that the code needs to be loaded before it takes effect.  If you change a file on disk, the game doesn’t know it changed until something tells it that it changed.  When you edit the tinker or config files through the web portal, the web portal is smart enough to reload everything for you.  But when you’re editing stuff on the server shell manually, you need to do that step.

To do that, we can type ‘load config’ to reload the configuration, or ‘load tinker’ to load a single plugin, or even ‘load all’ to reload everything - but that’s a little inefficient.

In this case we know what we changed, so we can just type load tinker to reload the tinker plugin.

Now that the new code has been loaded, when we type the tinker command we see our hello world message.

## Conclusion

So that’s how you edit code files on the game server directly.  It’s quick; it’s easy; you don’t have to install fancy tools - everything you need is already on the game server.  But there are some down-sides.

The first down-side is that the code editors that run on the command line, like nano, are pretty liimted.  You can’t click around with the mouse or cut and paste easily.  It’s hard to switch between files.  They’re very basic, which is fine if all you want to do is add ‘hello world’ to the tinker command, but if you want to do something more sophisticated - like writing an entire character creation system from scratch - the editor is going to get in your way.

The other down-side is that you’re changing the code on the game server.  So when you want to test it, you have to test it on the actual game.  Now if you do everything right, it’s not a big deal.  But if you mess something up - now you’ve messed up the code for everyone on the actual game.  Which is what we’re used to from Penn and Tiny, but it’s not necessarily the best way.

That concludes this tutorial.  In the next tutorial, we’ll look at some better options - starting with how you can use FTP to modify files on your PC and then upload them to the game.

Thanks for listening!
