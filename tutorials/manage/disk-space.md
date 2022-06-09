---
title: Freeing Disk Space
description: 
layout: page
---

As your server ages, you may find that accumulated junk has eaten away at your disk space. You might even get warnings about your server running low on disk space. If that happens, this article will help.

{% tip %}
All of these commands should be run in the server shell using your ares user.
{% endtip %}

## Quick Disk Space Cleanup

Here are some easy things to do that will quickly free up disk space:

- `sudo apt-get autoremove` - Removes old ubuntu packages that aren't needed.
- `sudo apt-get clean` - Clears the ubuntu package cache.
- `sudo journalctl --vacuum-time=10days` - Clears old log files. (You can customize the retention time.)

Sometimes you will accumulate older versions of node and ruby. You can remove the old ones, but be careful not to remove the versions that Ares is currently using:

- Show all node versions using `nvm list`.
- Remove any unused node versions (the ones that _don't_ have a green arrow next to them) in the above list using `nvm uninstall <version>`.
- Show all ruby versions using `rvm list`.
- Remove any unused ruby versions (the ones *without* an arrow or star next to them) using `rvm uninstall <version>`.

## Advanced Disk Usage

Generally the quick fixes above will be enough to sort out any disk space issues. If you find your disk space usage is still high, you can do more investigation.

{% warning %}
Use extreme caution when manually deleting files, especially if you are not comfortable with system administration. You may inadvertently put your droplet into a bad state by deleting something important.
{% endwarning %}

To assess disk space usage, you will want to install the NCDU disk tool:  `sudo apt-get install ncdu`

Then to get a report of disk space usage, run: `ncdu <directory>` (leave directory blank for your current directory).

This gives a report like so:

```
--- /home/ares -------------------------------------------------
    1.8 GiB [##########] /.rvm                                                     
  655.3 MiB [###       ] /ares-webportal
  311.8 MiB [#         ] /.nvm
  302.4 MiB [#         ] /aresmush
  217.4 MiB [#         ] /.npm
   18.0 MiB [          ] /.bundle

````

You can use the arrow keys to navigate through the directories to see more detail and see where your disk space is going.

For your Ares-related files, RVM, ares-webportal, and NVM should be taking up the bulk of your disk usage. Pruning these is already covered by "Freeing Disk Space" above.  The big hitter in aresmush will be your backups and file uploads.
