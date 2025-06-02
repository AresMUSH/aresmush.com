---
title: Web Portal Mixins
description: 
layout: page
tags:
- code
- webportal
---

Like the `include CommandHandler` statement on the game engine side, which allows all Command Handlers to share some common code, **Mixins** in Ember provide common building blocks of functionality.  There are a few common Mixins used throughout the web code.

{% note %} 
Instead of `include`, the Ember terminology is to `extend` a Mixin.
{% endnote %}

{% include toc.html %}

## Route Authentication

All Routes extend one of the route authentication mixins to make sure the character is properly authenticated.

* `DefaultRoute` is for routes that are allowed even if you're not logged in.
* `AuthenticatedRoute` is for routes that require you to be logged in.
* `RestrictedRoute` is for routes that require you to be logged in with an admin or coder character.
* `UnauthenticatedRouteMixin` is for routes that require you to **not** be logged in.  This one has a slightly different name than the others because it comes from another code library.

For example:

    import DefaultRoute from 'ares-webportal/mixins/default-route';
    export default Route.extend(DefaultRoute, {
      
### Authenticated Controller

The `AuthenticatedController` mixin provides some utility methods like `isApproved` that can be used in templates to control whether certain actions are allowed.

## Reload Model

Sometimes you want to refresh a route without leaving the screen, usually after sending a request to the game that updates a bunch of data.  For example, the chargen screen reloads itself after the player clicks the "Reset Abilities" button.

Any Controller can issue a refresh request by calling `this.send('reloadModel');`

## Route Reset On Exit

Some routes have form data that you want to clear when the player leaves the screen, such as the event creation form.  Otherwise it's a little weird if the player comes back six hours later and the form still has their previous data.  

Any controller can implement a `resetController` method on the controller to clear out its data whenever the player leaves the screen.  