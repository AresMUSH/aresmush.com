---
title: Resetting Forgotten Admin Passwords
description: 
layout: page
tags:
- manage
- password
- headwiz
---

If you've forgotten one of your admin passwords, there are a number of remedies depending on _which_ password you've forgotten.

{% include toc.html %}

## Forgotten Regular Admin / Player Password

Any admin can reset passwords using the `password/reset <name>` command. This will generate a new temporary password, which you can give to the other player.

## Forgotten Master Admin / Headwiz / God Password

The Master Admin (named Headwiz by default) is equivalent to the "God" character on other MUs, and has special privileges. Regular admins can't change Headwiz' password, so a special step is required.

### Game Method

If you have access to an admin with coder privileges, you can use code to change it.  (This is why you should only give coder privileges to trusted individuals; they have full control over the database.)

Just have your coder execute this command in-game:

    ruby  Login.set_random_password(Game.master.master_admin)

This will generate a new temporary password.

### Shell Method

If you don't have a coder character available, log into the server shell and change into the aresmush folder.  Run the following script with the desired new password:

    bin/script reset_headwiz_password,somenewpassword


## Forgotten Ares Shell Password

If you've forgotten your ares user password to the server shell, you can use the 'root' user to reset it.  Just login as 'root' and use `passwd ares` and enter a new password.

{% tip %}
This is one of the rare instances where you'll actually want to use the root user.  Most other Ares operations should be done with the 'ares' user.
{% endtip %}

## Forgotten Root User Password

Normally you don't need the root user password, because you should be using your ares user for everything.  But if you do ever forget it, you can reset it in your DigitalOcean droplet console. See the DO help article [reset droplet root passwords](https://www.digitalocean.com/docs/droplets/resources/reset-root-password/) for details.