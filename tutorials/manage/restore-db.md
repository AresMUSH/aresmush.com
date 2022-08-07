---
title: Restoring the Database
description: 
layout: page
tags:
- manage
- database
- backup
---

Setting up [automatic backups](/tutorials/manage/backups.html) of your game is important.  In the unlikely event that disaster strikes, you'll have a backup copy of your game's database and files. This article describes how to restore the game from a backup.

{% include toc.html %}

## Restoring from a DigitalOcean Weekly Backup

If you elected to use DigitalOcean's backup feature, see DO's [backups tutorial](https://www.digitalocean.com/community/tutorials/an-introduction-to-digitalocean-backups) for help restoring.

## Restoring Game Files

You can restore game configuration files, uploads, and everything else in the `aresmush/game` folder just by using a FTP client to upload files from your backup copy.  After the upload, run `load config` in-game to reload the configuration settings.

## Restoring the Database

To restore the database:

1. Stop the database service.  In the [server shell](/tutorials/install/server-shell.html), type `sudo service redis-server stop`.
2. Copy the `dump.rdb` file from your back copy into the database data path.  Typically this is `/var/lib/redis/dump.rdb`.  If you get a permission error, run `sudo chmod g+rwx /var/lib/redis/dump.rdb` from the server shell.  Sometimes redis resets the file permissions.
3. Restart the database service by typing `sudo service redis-server start` in the server shell.

{% note %} 
If you used a non-standard installation, your database commands and file path may be different than what's shown above.
{% endnote %}

## Restoring Code

If you use GitHub to store your code, you can use the `git` commands to clone a stable version of the code from your repository.

If you don't use GitHub, you'll need to manually restore the `aresmush` and `ares-webportal` folders, typically using FTP.