---
title: Coding in Ares
date: '2015-12-20'
layout: post
description:
categories:
tags: [feature]
author: Faraday
preview_image: coding-ares.jpg
teaser: Overview of coding in Ares.
---

The last article explained how (and why) code in AresMUSH uses Ruby rather than MUSH softcode. You don't edit the code "live" through the MUSH windows. So how **do** you code?

For those who have only ever done MUSH coding, the easiest analogy is to think of Ares code like the MUSH "news" or "help" files. They are just plain text files that live on the server. You have several options for managing them:

1) Connect to the server (using telnet or SSH) and edit them there.
2) Edit them on your local computer and FTP them to the server.
3) Use a version control system.

We recommend the third option. Version control is just good practice for all kinds of software. It lets you **collaborate** easily with other coders, and gives you a **history** of what changed and why.

> New to version control? Check out [this visual guide](http://betterexplained.com/articles/a-visual-guide-to-version-control/).

AresMUSH uses [GitHub](https://github.com/). When you first install Ares, you will have the option to create your own version-controlled copy of the code. This is called a "fork" in GitHub lingo, like a fork in the road. Your code goes off one way, the main Ares code goes off in another, but they share a common path up until that point.

{% include pretty_image.html file='postpics/fork.png' max-width="200px" %}

Using GitHub gives you a central place to store your game's code. Any of your coders can download the code to their hard drive, change it, and upload it back to GitHub.

Once it's in GitHub, you can use Ares commands to load the latest code into the game -- without telnetting into the server, and without rebooting the game<sup>(*)</sup>!

By the way, this is the same model that most coding (outside of MUSHes) follows.  That means there are lots of tutorials out there, and anyone who does this sort of thing in RL should be able to adapt pretty easily.

<small>(*) - Changes to the AresMUSH engine code do require a reboot, but that should rarely or never happen. 99% of your changes will be to the plugin code, which can be loaded while the game is running.</small>