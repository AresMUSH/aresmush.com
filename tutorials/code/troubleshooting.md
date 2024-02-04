---
title: Troubleshooting Issues
description: 
layout: page
tags:
- code
- troubleshooting
---

Sometimes things go wrong, and you'll get the "Sorry! The code lost its mind while executing a command..." message or the Sad Picard screen on the web portal.  This article will help you diagnose the problem.

If the information below doesn't help you, you can always ask for help on the [Ares Forums or Discord](/feedback.html).

{% include toc.html %}

## Log Files

The first place to check is the game log.  Most errors will add an entry in the log file telling exactly what the problem is.  You have several options for checking the log:

* Go to Admin -> Logs on the web portal.  The highest-numbered log will be the most recent, but you may want to look at the one prior as well.
* In the server shell, look in the `aresmush/game/logs` directory.  You can use a unix terminal text editor like nano to open them, or FTP them to your PC.
* In the MU client, the `debuglog` command will show you only the most recent log entries.

Once you have the log file open, search for `ERROR`.  You'll see some code stuff that may look like gibberish:

    2018-02-20 04:21:39 ERROR - Error in Web Request: client= error=private method `select' called for nil:NilClass backtrace=[
    "/home/ares/aresmush/plugins/arescentral/web/get_players_handler.rb:13:in `block in handle'", 
    "/home/ares/.rvm/gems/ruby-2.4.1/gems/ohm-3.0.3/lib/ohm.rb:123:in `block (2 levels) in each'", 
    "/home/ares/aresmush/plugins/arescentral/web/get_players_handler.rb:11:in `handle'", 
    "/home/ares/aresmush/engine/aresmush/commands/dispatcher.rb:125:in `block (2 levels) in on_web_request'", 
    "/home/ares/aresmush/engine/aresmush/commands/dispatcher.rb:119:in `each'"]

The first line is the one that gives the specific error (in this case - an object was `nil` when it shouldn't have been). The remaining lines help identify what the code was doing at the time (in this case - inside the /players web handler).

Check the list of common issues below to see if your error matches any of those. If not, you can always [ask for help](/feedback.html).

<a name="browser-console"></a>

## Browser Console

All major browsers have tools built in to help developers debug their Javascript. This can help you diagnose web issues.

In Chrome, the dev tools are under View -> Developer -> Developer Tools. In other browsers, look for a "Developer" menu (or do a Google search for "(yourbrowser) developer tools").

{% include pretty_image.html file='code/web-debug-console.png' %}

For help troubleshooting your custom web code, see [Debugging Custom Web Requests]({{site.baseurl}}/tutorials/code/web-debug.html).

## Common Issues

### YAML Issues

The configuration files use YAML, and there are several common issues that can result from trouble with your game configuration.  Often you'll see an error message like "Error reading YAML from fs3combat.yml...", but any error that happens right after you changed your game configuration should make you suspect a YAML problem.  See [Troubleshooting YAML](/tutorials/code/troubleshooting-yaml.html) for more details.

### Port In Use

Sometimes you'll see an error in the logs like "Couldn't start the game: error=no acceptor (port is in use or requires root privileges)".  This usually means:

1. Your game is already started.  Maybe it auto-started after a reboot and you're unnecessarily trying to start it again.
2. There is a problem with the IP or hostname you specified.  For an IP, make sure you gave the public IP address.  For a hostname, make sure that the DNS is properly configured and that `nslookup YOURHOSTNAME` returns the correct IP address.  It can take up to 24 hours for a new DNS record to be visible to the droplet, and Ares won't work until that happens.
3. You have an issue with your Ares port configuration. Remember that Ares needs multiple ports, and they all have to be different.  You can't use the same port number for both your telnet server and engine API, for instance.

If none of that helps, [ask for help](/feedback.html). There are some other unusual configuration issues that can cause that issue.

### Server Won't Start

Sometimes you'll get a 'connection refused' error in your MU client or a 'This site can't be reached' error in your web browser.  When this happens, there are a few things to check:

* Make sure your hostname is correct and your DNS is set up.  Ares can't start if the hostname is inaccessible.
* Try starting the game in [Debug Mode](/tutorials/code/debug-mode.html) and see if there are any additional errors on the server console.

### Database Issues

If your game can't connect to the database you'll see an error like:  "Error connecting to database. Check your database configuration."   Here are a few things to try:

* Check your database config file (database.yml) and make sure you have the correct URL (usually "127.0.0.1:6379").
* Check your secrets config file (secrets.yml) and make sure your database password has been set.
* Make sure your database service is running.  You can use the server shell command `service redis-server status`.
* Check your redis configuration. In the standard install, this file lives in `/etc/redis/redis.conf`. The last few lines typically look like this, with a password matching what's in secrets.yml.

```
  aof-rewrite-incremental-fsync yes
  # Generated by CONFIG REWRITE
  requirepass YOURPASSWORD
```

### Web Portal Unavailable

If you get a 'page not found' error for your web portal, here are some things to check:

* Make sure that your web server is running.  You can use the server shell command `service nginx status`.
* Make sure that the website code successfully deployed. Run a `website/deploy` command from the client and see if there are any errors.

If none of that helps, [ask for help](/feedback.html) and we can walk you through checking your web server configuration.

### Web Portal Can't Connect to the Game

Sometimes you'll get a Sad Picard message saying the web portal can't connect to the game.  
  
* Make sure the game is actually running and you can connect to it with a MU client.
* Try it in a private/incognito browser window to avoid any Javascript cache issues.

### Web Portal Sad Picard

Web portal errors are reported with the Sad Captain Picard screen saying "Oops! Something went wrong with the website." Most of the time, problems on the web portal are actually problems in the web request on the game side.  You'll see those errors in the game log and troubleshoot them in the same way you would any other game error.  Occasionally, though, the problem will be in the web portal Javascript code.  

* Make sure the game is actually running and you can connect to it with a MU client.
* Try it in a private/incognito browser window to avoid any Javascript cache issues.
* Check the [Browser Console](#browser-console) for errors.

### Web Sockets Not Working

If you get a warning saying "The website is not receiving live updates from the game", it means that the websocket connection allowing real-time updates between the web page and the game isn't working.  Regular page requests will be fine, but 'live' updates like scene poses or alerts about new mail messages won't come through.

* Try a [force-refresh](https://en.wikipedia.org/wiki/Wikipedia:Bypass_your_cache) in your web browser.
* Check the [Browser Console](#browser-console) for errors.
* If nobody's websockets are working, try shutting down and restarting the game engine.

### Certificate Expired

If you are using HTTPS for your web portal, a common reason for getting "The website is not receiving live updates from the game" is that your security certificate has expired.  If this happens, you will see a `ERR_CERT_DATE_INVALID` in the browser developer tools.

Shutting down and restarting the game engine usually fixes this.  If not, just go to the aresmush directory and re-run `bin/certs <your domain name>`.
  
### Web Portal Stuck on Old Version

Sometimes you'll do an upgrade and you'll see mismatched versions between the game and the web portal (on the bottom of all portal pages):

    AresMUSH game v0.70, portal v0.69

The web portal and game engine always have to have the same version.  If they don't, you will get unpredictable errors.

There are several possible causes:

1. **Browser Cache** - Try to open the web portal in a private/incognito browser window.  Sometimes your browser is stubbornly holding onto the old Javascript and needs a kick.
2. **Deploy Failed** - Try to re-deploy the website using the `website/deploy` command in-game or by running `bin/deploy` from the ares-webportal directory on the server shell.  This will tell you if you missed any weird errors when the website was published.
3. **Update Fork** - If your own private code fork, make sure you updated the webportal code too.  Sometimes folks forget and only update the game engine code.
4. **Restart Server** - Try restarting your entire server as described [here](https://aresmush.com/tutorials/manage/reboot.html).

A successful website deploy will end with a list of files, like this:

```
Built project successfully. Stored in "dist/".
File sizes:
 - dist/assets/ares-webportal-5d9f5985e1460779a552cf47f222971d.css: 143.77 KB (23.25 KB gzipped)
 - dist/assets/ares-webportal-7d7c53430414e59c856937e57e284827.js: 894.15 KB (98.25 KB gzipped)
etc.
```

### Key Not Found Error on Approval or Roster Claim

You may see the approval welcome message or roster claim message not appearing, and a key error in the log:

    error=key{position} not found
    error=key{faction} not found

This means your welcome messages are configured to use a group that doesn't exist.  Probably you changed your groups from the default (position/faction) and just need to update the messages in [idle config](https://aresmush.com/tutorials/config/idle.html#roster_welcome_msg) and [chargen config](https://aresmush.com/tutorials/config/chargen.html#messages).  
  

### Error Using Includes

When using includes, sometimes your wiki page will say: "There was a problem including (some include page)."  

* Make sure the include page exists and there are no typos in the name.
* Make sure you are passing all necessary variables to the include. The error message will hopefully give you a tip as to what variable is missing.

Sometimes you get this strange error: Error loading include (some include page) : malformed format string - %;

That means there's a stray "%" somewhere in your include page.  You need to make all raw %'s into %% so they are formatted appropriately.

## Web Portal Warnings

When you deploy the web portal, you may see any or all of the following warnings that you can safely ignore.

### fsevents

```
npm WARN optional SKIPPING OPTIONAL DEPENDENCY: fsevents@1.2.9 (node_modules/fsevents):
npm WARN notsup SKIPPING OPTIONAL DEPENDENCY: Unsupported platform for fsevents@1.2.9: wanted {"os":"darwin","arch":"any"} (current: {"os":"linux","arch":"x64"})
```

fsevents is an optional dependency for one of the javascript libraries we use.  Its absence doesn't affect anything.

### Watchman

```
Could not start watchman
```

Watchman is an optional tool for local debugging; it doesn't apply to your server.

### Node Version Untested

```
WARNING: Node v11.0.0 is not tested against Ember CLI on your platform. We recommend that you use the most-recent "Active LTS" version of Node.js. See https://git.io/v7S5n for details.
```

If you're using 11.0, it's been extensively tested for Ares and works just fine.  If you've got some other weird version of node you might want to use 12.x, which is the LTS version.

### NPM Audit

```
audited 218632 packages in 30.459s
found 69 vulnerabilities (11 low, 26 moderate, 32 high)
  run `npm audit fix` to fix them, or `npm audit` for details
```

The NPM audit warnings come from off-the-shelf javascript libraries. We do our best to keep up with security issues, but most of these come out of EmberJS and its dependencies and are not Ares-specific. Others apply to features Ares isn't using, so we don't need to worry about them.

## Debug Mode

For tricky issues - especially during development - it can be helpful to run the game in [Debug Mode](/tutorials/code/debug-mode.html).