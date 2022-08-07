---
title: Coding for Ares
description: 
layout: page
---

These articles will teach you how to code for AresMUSH.  

{% include tutorial_warning.html %}

## Introduction

* [Ares Architecture](/tutorials/code/architecture.html) - All the moving parts that make up an Ares game.
* [Coding for Ares](/tutorials/code/overview.html) - General overview of how coding for Ares works.

## Basic Coding Tutorials

There are several tutorials designed to introduce you to Ares coding step by step.  It's recommended that you do these in order, since they all build on each other.

### Tutorial #1 - Quickstart

Learn the basic Ares functions and code concepts.

<button data-toggle="collapse" data-target="#quickstart" class="btn btn-info">Show Tutorial</button>

<div id="quickstart" class="collapse">
{% include quickstart_tutorial.html %}
</div>

### Tutorial #2 - Editing Ares Code

Learn what tools you use to edit the Ares code.

<button data-toggle="collapse" data-target="#edit-code" class="btn btn-info">Show Tutorial</button>

<div id="edit-code" class="collapse">
{% include edit_code_tutorial.html %}
</div>

### Tutorial #3 - Adding a Command (Character Goals)

Learn how to add a command (a simple 'goals' command to set character goals.)

<button data-toggle="collapse" data-target="#add-cmd" class="btn btn-info">Show Tutorial</button>

<div id="add-cmd" class="collapse">
{% include add_command_tutorial.html %}
</div>

### Tutorial #4 - Creating a Plugin (Cortex Skills System)

Learn the anatomy of a more complex system (aka a plugin) from start to finish.  The example uses the Cortex skills system.

<button data-toggle="collapse" data-target="#create-plugin" class="btn btn-info">Show Tutorial</button>

<div id="create-plugin" class="collapse">
{% include create_plugin_tutorial.html %}
</div>

### Tutorial #5 - Modifying the Web Portal (Web Goals)

Learn how to add things - in this case, the character goals from Tutorial #3 - to the web portal. 

<button data-toggle="collapse" data-target="#add-web" class="btn btn-info">Show Tutorial</button>

<div id="add-web" class="collapse">
{% include add_web_tutorial.html %}
</div>

## Advanced Coding Topics

Once you've completed the initial tutorials, there are a wealth of other topics available for reference. 

{% tip %} 
It's suggested that you refer to these as you need them rather than trying to learn them all at once.  There's a lot of information here and it can be a bit overwhelming.
{% endtip %}

### General

* [Basic Concepts](/tutorials/code/concepts.html)
* [Tinkering](/tutorials/code/tinker.html)
* [Using Formatting Codes](/tutorials/code/formatting.html)
* [Using Log Files](/tutorials/code/logs.html)

### Language Resources

* [Learning Ruby](/tutorials/code/ruby.html)
* [Learning EmberJS](/tutorials/code/ember.html)

### Configuration

* [Enabling and Disabling Plugins](/tutorials/config/plugins.html)
* [Understanding YAML](/tutorials/code/yaml.html)
* [Troubleshooting YAML](/tutorials/code/troubleshooting-yaml.html)
* [Shortcuts](/tutorials/code/shortcuts.html)
* [Recovering from Config Errors](/tutorials/config/config-errors.html) - Rolling back defaults if your config gets messed up.

### Engine

* [Engine Ports](/tutorials/code/ports.html)
* [Engine Globals](/tutorials/code/globals.html)
* [Client Monitor](/tutorials/code/client-monitor.html)
* [Config Reader](/tutorials/code/config-reader.html)
* [Cron Jobs](/tutorials/code/cron.html)
* [Help System](/tutorials/code/help.html)
* [Localization](/tutorials/code/localization.html)
* [Notifications](/tutorials/code/notifications.html)
* [Dispatcher](/tutorials/code/dispatcher.html)

### Database

* [Database](/tutorials/code/database.html)
* [Database Relationships](/tutorials/code/db-relationships.html)
* [Database Indices](/tutorials/code/db-indices.html)
* [Editing the Database](/tutorials/code/edit-database.html)
* [Removing a Database Field](/tutorials/code/db-remove-field.html)
* [Database Migrations](/tutorials/code/db-migration.html)

### Plugins and Commands

* [Plugins](/tutorials/code/plugins.html)
* [Command Handling](/tutorials/code/commands.html)
* [Arg Parsers](/tutorials/code/arg-parsers.html)
* [Error Checkers](/tutorials/code/error-checkers.html)
* [Event Handling](/tutorials/code/events.html)
* [Web Request Handling](/tutorials/code/web-requests.html)
* [Custom Code](/tutorials/code/custom.html)
* [Reloading Code](/tutorials/code/reload.html)

### Utilities

* [Emitting](/tutorials/code/emitting.html)
* [Formatters](/tutorials/code/formatters.html)
* [Multi-Page Output (Paginator)](/tutorials/code/paginator.html)
* [Templates](/tutorials/code/templates.html)
* [Config Validation](/tutorials/code/config-validator.html)

### Web Portal

* [Web Portal Overview](/tutorials/code/web-portal.html)
* [Web Portal Routes](/tutorials/code/web-routes.html)
* [Web Portal Templates](/tutorials/code/web-templates.html)
* [Web Portal Controllers](/tutorials/code/web-controllers.html)
* [Web Portal Services](/tutorials/code/web-services.html)
* [Web Portal Mixins](/tutorials/code/web-mixins.html)
* [Game Api](/tutorials/code/web-game-api.html)
* [Web Request Handling](/tutorials/code/web-requests.html)
* [Navigation](/tutorials/code/web-nav.html)
* [Wiki Extensions](/tutorials/code/wiki-extensions.html)

### Troubleshooting

* [Troubleshooting Issues](/tutorials/code/troubleshooting.html)
* [Debug Mode](/tutorials/code/debug-mode.html)
* [Debugging Custom Web Requests](/tutorials/code/web-debug.html)

## FS3

* [FS3 Code Roadmap](/tutorials/code/fs3-roadmap.html) - Overview of the FS3 code.
* [Replacing FS3](/tutorials/code/replacing-fs3.html) - Replacing FS3 with your own skills system.

## Contributions

* [Community Contributions](/tutorials/code/contribs.html) - Using community plugins.
* [Submitting Contributions](/tutorials/code/submit-contribs.html) - Submitting your own contribs.

## Miscellaneous

* [Chopping Block](/tutorials/code/chopping-block.html) - Code that didn't make the cut.
* [Custom Code Hooks](/tutorials/code/custom-hooks.html) - Places where you can easily tie in your custom code.
* [Using Git](/tutorials/code/git.html) - Using the GitHub version control system to manage your code.
* [Setting up a Development System](/tutorials/code/dev-tools.html) - Setting up a system to code and test.
* [Running Tests](/tutorials/code/tests.html) - Running the automated unit tests.
* [Telnet Extensions](/tutorials/code/telnet-extensions.html) - About telnet extensions and MCP.
