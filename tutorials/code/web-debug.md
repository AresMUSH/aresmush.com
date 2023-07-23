---
title: Debugging Web Requests
description: 
layout: page
tags:
- code
- webportal
---

When making your own custom web portal pages and requests, inevitably something will go wrong. This tutorial will help you debug your own portal code.

{% include toc.html %}

## Journey of a Web Request

Before you start debugging, it's helpful to understand all the 'legs' that your data goes through on its trip from the web portal to the game and back again.

1. The web portal sends a request to the game. Usually this comes out of either an Ember controller [in response to an action](/tutorials/code/web-controllers.html#controller-actions) or an Ember route when [loading its model](/tutorials/code/web-routes.html).
2. The game dispatcher routes that request to the plugin who wants it based on the [plugin's dispatch method](/tutorials/code/web-requests.html#handling-web-requests)
3. The request is handled by a [web request handler](/tutorials/code/web-requests.html#request-handler-classes) using the class specified in the prior step.
4. The request handler returns data, which gets back to whatever Ember component requested it (the route or the controller). Controllers tend to just do something immediately with the data. Routes put the data into their 'model' property.

When debugging, we can check along each leg of the journey to make sure that the requests and data are getting where they're supposed to go.

<a name="browser-dev-tools"></a>

## Using the Browser Developer Tools

All major browsers have tools built in to help developers debug their Javascript. This includes:

* An inspector to look at page elements and styles.
* A debug console where JS errors and log messages will appear.
* A network log of traffic between the game and the browser.
* A code debugger.

In Chrome, the dev tools are under View -> Developer -> Developer Tools.

If you install the [Ember Inspector](https://chrome.google.com/webstore/detail/ember-inspector/bmdblncegkenkacieihfhpjfppoconhi?hl=en), your developer tools will include a special Ember tab that helps you debug EmberJS apps like the web portal.


## Debugging Tips

Here are some specific steps to go through when debugging the portal.

### Check the Logs

Rule out the obvious first.

1. Check the game debug log under Admin -> Logs in the web portal (see [troubleshooting](/tutorials/code/troubleshooting.html)  for details)
2. Check the browser console for errors.

{% include pretty_image.html file='code/web-debug-console.png' %}


### Check the Game Handler

Put a debug message into the web request handler.  This will tell you that the request got routed to your handler properly.

    class SomeWebRequestHandler
      def handle(request)
        Global.logger.debug "Got #{request.cmd} #{request.args}"
        
        # Return your data normally here.
      end
    end

Not seeing the message?  Make sure there are no typos in the command name, and that your plugin's `get_web_request_handler` method is returning the appropriate class.

### Check the Request Data

In your browser's developer console, you can see the traffic between the game and the browser.

1. Open the [browser dev tools](#browser-dev-tools) and go to the "Network" tab.
2. Once the network tab is open, reload the page or re-trigger the action that generates the request.
3. Find the most recent requests (usually they'll be at the bottom of the list).
4. Check the most recent ones, one by one, until you find the request you're interested in. You're looking for the one whose "cmd" matches the command you want.

{% include pretty_image.html file='code/web-debug.png' %}

You can see the command arguments in the Form Data section.  The response in shown in the "Response" tab as a JSON string. You can use a tool like [JSON Formatter](https://jsonformatter.org/) to pretty it up.

{% include pretty_image.html file='code/web-debug-response.png' %}

Common issues to check for:

* The command name in the request is incorrect.
* Some args are missing.
* The response data isn't formatted in the way you expect. (this problem is on the game side)

### Check the Client Handling

In a controller, you can use a Javascript `console.log` statement or the browser debugger to step through the code and see what's going on.

The web portal code is found in the source tab under your hostname (e.g., localhost:4200) -> assets -> ares-webportal. Using the browser tools, you can set breakpoints in controllers/components, and look at variables as the code executes.

{% include pretty_image.html file='code/web-debug-source.png' %}

It's very difficult to debug a route this way. Instead, you'll want to use the [Ember Inspector](#browser-dev-tools). 

Go to the "Routes" tab, find your route, and click on the little "$E" next to route. This will print out the route's data to the console.

{% include pretty_image.html file='code/web-debug-ember.png' %}

Click the little `>` next to the Ember console printout to expand the route data. Usually you'll be looking for the `currentModel` property, which shows the route's model.

{% include pretty_image.html file='code/web-debug-ember2.png' %}

Common issues to check for:

* The controller is throwing an error, which you'll see on the browser debug console.
* The route data is not what you expected.

### Check the Template

Finally check the web template for display errors. Try replacing what's there with a simple "Hello World" string just ot make sure you're loading the right template page.

Common issues to check for:

* The template is missing `this.` when accessing variables.
* The HTML syntax is wrong; this can prevent the web portal from deploying.
* The data is not in the place you expect - maybe it's using `model.foo` but should be `model.char.foo`.


### Web Portal Debug Mode

If you're running in a local test environment, it can be helpful while testing to run the web portal in [Debug Mode](/tutorials/code/debug-mode.html#web-portal), so you don't have to re-deploy the portal every time you change the code.