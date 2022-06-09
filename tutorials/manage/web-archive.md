---
title: Archiving the Web Portal
description: 
layout: page
tags:
- manage
- backup
- webportal
---

All games come to an end eventually, and when that happens you don't want to lose your entire website.  

## Creating a Portal Archive

Ares allows you to export the key bits of the web portal to disk:  Characters, Scenes and Wiki.  

See 'help wiki archive' in your in-game help files for details.

If you do have your archive available publicly, you may [contact Faraday](/feedback.html) to have it linked to the [AresCentral game archive](https://arescentral.aresmush.com/wiki).

(For older games, run `bundle exec rake webexport` from the server shell's aresmush directory, and the output will be in the wiki-export folder.)

## Archiving Wiki Markdown

You can also export just the raw markdown files for just the wiki.  This is helpful if you ever want to use the wiki files again on another game, or just want a copy for local reading:

    bin/script export_wiki_markdown

The files will be in the wiki-md directory, which you can then FTP to your PC.