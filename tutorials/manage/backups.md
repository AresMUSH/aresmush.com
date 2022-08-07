---
title: Backing Up the Game
description: 
layout: page
tags:
- manage
- database
- backup
---

It's important to make backups of your game database and files.  There are many ways to do this, a few of which are discussed here.  

{% include toc.html %}

## What Do I Need to Back Up?

Here are the things that you need to back up in order to protect your game from disaster:

* The database, located in `/var/lib/redis/dump.rdb`.
* The game files, located in `/home/ares/aresmush/game`. This includes your config, styles and web portal file uploads.

The file locations above assume you used the automated install. If you did a custom installation, hopefully you know where you put things.

{% note %} 
Ares' automated backup tools do not include source code.  It's assumed you're either using GitHub for source control or uploading things from your local computer.
{% endnote %}

## Backup Options

Ares has several backup options available to you, each with their own pros and cons.

### Local Backups

By default, Ares is configured to perform nightly backups, stored in the `/home/ares/aresmush/backups` directory. It will keep the last few days of backups.

This offers you some protection against someone messing up your database or accidentally deleting some files, but it doesn't help you if your server suffers a catastrophic failure or if you want a backup from a month ago.

For added backup security, you can FTP these files to your PC's hard drive; you just need to remember to do so.

### DigitalOcean Automatic Backups

If you are using a DigitalOcean droplet, you can use their [Automatic Backup](https://www.digitalocean.com/community/tutorials/an-introduction-to-digitalocean-backups) feature to create a weekly backup of your entire server.  This includes the database, the code, the server config - everything.  

This is the most robust form of backup strategy, but it costs a little extra.  As of 2/18, automated weekly backups of the standard Ares droplet size cost $1/month.

### Automatic Backups with S3

AresMUSH can automatically perform daily backups to Amazon's S3 storage service for a safe, off-site storage solution. 

{% note %} 
AWS is a great backup option, but AWS' menu options can be overwhelming for novice server admins.  Make sure you're familiar with their cost tiers.  Most games <b>should</b> fit comfortably into their 'free tier' and cost you nothing; however, it's your responsibility to understand their pricing tiers and know what you're signing up for.
{% endnote %}

#### Setting up S3

To set up automatic backups, you'll need:

1. An account with Amazon Web Services.
2. An AWS S3 Bucket.  (which is like a folder to store your files)
3. An AWS access key.

You'll need to follow the Amazon tutorials, particularly [Getting Started With S3](http://docs.aws.amazon.com/AmazonS3/latest/gsg/AmazonS3Basics.html) and [Managing Access to S3](http://docs.aws.amazon.com/AmazonS3/latest/dev/intro-managing-access-s3-resources.html).

{% note %} 
Even if you use S3 for other things, create a separate bucket just for your AresMUSH backups.  Ares will delete older files to make room for new backups, and you don't want it to accidentally delete anything important!
{% endnote %}

#### Configuring the Game to Use S3

Once you have an S3 account, you'll need to configure the game to use it.

1. Go to the Web Portal's Admin screen.  
2. Select 'Setup'.
3. Select 'secrets.yml'.

Enter your AWS access key, bucket name and the code for the region your bucket is in into the AWS section.  You can find the AWS region codes [here](http://docs.aws.amazon.com/general/latest/gr/rande.html#apigateway_region).

#### Test the Backup

There are many moving parts in the AWS backup process.  Once you have it all set up, we recommend that you test it once using the manual `dbbackup` command.  Make sure that the database file ends up in your S3 bucket successfully before relying on the automatic daily backups.

## General Backup Configuration

For the automated backup strategies (local or AWS), there are a few things you'll want to configure.

1. Go to the Web Portal's Admin screen.  
2. Select 'Setup'.
3. Select `backup.yml`.

#### Backup Type

Set the backup type to 'aws' for AWS backups and 'local' for local backups.

#### Number of Backups

You can configure the number of backups the game keeps.  By default this is 5.  The game will only keep this many backup files.

{% note %}
If you _reduce_ the number of backups from its previous value, you need to manually remove any extra backup files.
{% endnote %}

#### Backup Cron Job

You can configure when backups are done.  By default it's early morning, after peak MU* times.  See the [Cron Job Tutorial](http://www.aresmush.com/tutorials/code/cron.html) for help if you want to change this.

#### Database File Location

If you used the standard install scripts, the game should already be configured with the proper database file location.  But if you performed a custom installation, you'll need to tell the game where the database file is.

1. Go to the Web Portal's Admin screen.  
2. Select 'Setup'.
3. Select `database.yml`.
4. Enter the path to redis' dump file.

## Restoring Backups

In the event you need to restore a backup, see [Restoring Backups](/tutorials/manage/restore-db.html).