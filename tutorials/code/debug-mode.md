---
title: Debug Mode
description: 
layout: page
tags:
- code
---

Both the game and the web portal have a **debug mode** that is helpful when developing code.

## Game Debug Mode

To start the game in debug mode, run `bin/devstart` from the aresmush directory.  Debug mode is helpful because it prints error messages directly to the server shell window.  When something goes wrong, you can flip over to the shell and see the problem immediately without needing to browse through log files.

The debug game will run until you close the server shell or hit CTRL-C.  You can restart the game using `bin/startares` once you're done.

{% note %} 
The game must be shut down before you can run it in debug mode.  Otherwise you'll get a 'port already in use' error.
{% endnote %}

### Debugging with HTTPS

The regular 'devstart' is not compatible with HTTPS.  If your game is using HTTPS, you'll need to start debug mode using `bundle exec rake startares`.

<a name="web-portal"></a>

## Web Portal Debug Mode

The web portal also has a debug mode, which you can activate using `bin/devportal` from the ares-webportal directory.  The cool part about the portal's debug mode is that the website will automatically reload as you change the code.  This lets you easily test your changes.

The debug portal will run until you close the server shell or hit CTRL-C.

{% note %} 
The portal's debug mode runs on port **4200**, so you access it like:  http://mygame.aresmush.com:4200.  The real portal can still be running while you have debug mode going, but you need to remember to do a `bin/deploy` to deploy your changes when you're finished.
{% endnote %}

### Dev Console

Your browser's developer console can also be helpful in debugging portal code.  To activate it in Chrome, go to View -> Developer -> Developer Tools.  This will open the dev console at either the bottom or side of your browser window.

The 'Elements' tab lets you inspect the CSS style of screen elements.  This is helpful if you want to override formatting with a [custom CSS style](/tutorials/config/website.html).

The 'Console' tab will show any Javascript errors that crop up.

The 'Sources' tab lets you set breakpoints and debug your code live as it runs.

The 'Network' tab traces server traffic, and can be used to analyze the contents of web requests to the game (and their responses).



