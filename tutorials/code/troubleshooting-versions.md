---
title: Troubleshooting Mismatched Versions
description: 
layout: page
tags:
- code
- troubleshooting
---

Sometimes you'll do an upgrade and you'll see mismatched versions between the game and the web portal (on the bottom of all portal pages):

    AresMUSH game v1.12.0, portal v1.11.0

The web portal and game engine always have to have the major and minor version (the first two numbers). If they don't, you will get unpredictable errors. The third number, the patch version, is allowed to differ. 

There are several potential causes for the version mismatch. The sections below shows steps to rule out each potential cause.

## Browser Cache

Sometimes your browser is stubbornly holding onto the old Javascript and needs a kick.

* Open the web portal in a private/incognito browser window.
* If this fixes the version mismatch, you're done! The game is fine; it was just a browser glitch.

## Failed Web Deploy

Sometimes the web portal doesn't deploy.

* Run `website/deploy` command from the clint `bin/deploy` from the ares-webportal directory on the server shell. (Don't use the web portal update button.)
* A successful website deploy will end with a list of files, as shown below.
* If you don't see the list of files, examine the output for errors and troubleshoot those.

A successful deploy ends with a list like the following:

```
Built project successfully. Stored in "dist/".
File sizes:
 - dist/assets/ares-webportal-5d9f5985e1460779a552cf47f222971d.css: 143.77 KB (23.25 KB gzipped)
 - dist/assets/ares-webportal-7d7c53430414e59c856937e57e284827.js: 894.15 KB (98.25 KB gzipped)
etc.
```

## Missed Fork Update

Sometimes folks forget to update their custom GitHub fork before updating the game. 

{% tip %}
If you don't have a separate fork, this doesn't apply; skip to the next section.
{% endtip %}

* Look **in your custom GitHub fork** to make sure that `aresmush/version.txt` is the correct version.
* Repeat for `ares-webportal/public/scripts/aresweb-version.js`.
* If either version is wrong, [update your fork](/tutorials/manage/upgrades.html#fork) and re-do the deployment.

## Failed GitHub Update

Sometimes the server doesn't get the right files from GitHub.

* In the server shell, run the following commands to examine the server-side version files:

```
cat aresmush/version.txt
cat ares-webportal/public/scripts/aresweb_version.js 
```

* If the versions match, go back to "Failed Web Deploy" and check again for errors.
* If one of the versions is outdated, run a git status and pull in that directory. For example:

```
cd ares-webportal
git status
git pull
```

* If there are any weird errors on either git command (like a [merge conflict](/tutorials/code/git-conflicts.html#merge) or [diverged branches](/tutorials/code/git-conflicts.html#diverged)), troubleshoot that error.


This will tell you if you missed any weird errors when the website was published.
3. **Update Fork** - If your own private code fork, make sure you updated the webportal code too.  Sometimes folks forget and only update the game engine code.
4. **Restart Server** - Try restarting your entire server as described [here](https://aresmush.com/tutorials/manage/conflicts.html).

A successful website deploy will end with a list of files, like this:


