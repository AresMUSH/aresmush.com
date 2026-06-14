---
title: Configuring the Game Wiki
layout: page
tags:
- config
---

The Web Portal wiki has a number of configuration options.  To set them:

1. Select Admin -> Setup
2. Edit `website.yml`.

{% include toc.html %}

## wiki_nav

You can provide a list of wiki pages to show in the Wiki dropdown menu.  Just give the page names one by one as a list.  For example:

    - Home
    - Getting Started
    - Policies

## restricted_pages

You can lock down certain pages on the wiki so they can only be edited by people with the `manage_wiki` permission.  Just list the page names one by one in list format.  You can also use `category:*` to restrict an entire category.  For example:

    - home
    - theme:*

## wiki_aliases

You can create aliases for redirects or commonly-misspelled wiki page names to avoid broken links.  Just list the alias and the page you want it to go to.  In this example, someone linking to 'main' will be directed to 'home' instead:

    main: home
    

## public_wiki_folders

Normally, players can only upload to the folder that matches their name, and admins can upload to any folder. You can optionally create other shared public folders that anyone can upload to. In the default installation, the `misc` folder is public.

    public_wiki_folders:
    - misc
    
## default_public_folder

This is the folder that the wiki file upload screen defaults to when you're uploading from the Files section. (When uploading files from a character page, it defaults to that character's folder.)

This should be a public folder from `public_wiki_folders`.

    default_public_folder: misc


## uploadable_extensions

Regular players who are not wiki admins can only upload images to the wiki by default.  You can configure the specific allowable file extensions with this setting.  They all must be in the format `*.jpg` or `*.png`. 