---
title: Archiving the Web Portal
description: 
layout: page
tags:
- manage
- backup
- webportal
---

All games come to an end eventually, and when that happens you don't want to lose your entire website.  Ares allows you to export the key bits of the web portal to disk:  Characters, Scenes and Wiki.  

The exporter doesn't fully re-create the web portal, and it's not perfect.  Some internal links may not function right and may require manual tweaks if you want a pristine archive.  The exporter just does the heavy lifting for you.

## Creating a Web Portal Archive

To run the exporter, go to the `aresmush` folder on the Server Shell and type:

> bundle exec rake webexport

{% tip %} 
If you've made extensive changes to the web portal styles and/or templates, you may need to tweak the code in  `aresmush/plugins/website/wiki_exporter.rb`  to get the exported files to look similar to your web portal.
{% endtip %}

This generates raw HTML files in the `wiki_export` folder.

## What to Do With Your Archive

First, you'll want to use FTP to download the web archive to your local PC for safekeeping.  You can browse the files locally just by double-clicking on `index.html`.

You can also make a ZIP file and share it with your players using DropBox or another file-sharing service so they can download the archive for themselves.  Since it's web pages, you could even host the archive on a static web server (using [Amazon S3 static web hosting](https://docs.aws.amazon.com/AmazonS3/latest/dev/WebsiteHosting.html) or a similar service).

If you do have your archive available publicly, [contact Faraday](/feedback.html) to have it linked to the [AresCentral game archive](https://arescentral.aresmush.com/wiki).