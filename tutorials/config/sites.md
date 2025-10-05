---
title: Configuring Banned Sites
layout: page
tags:
- siteban
- suspect
- trouble
- config
---

You can register certain IPs or hostnames as banned or suspect to block/alert you to problem players.  

To learn more about how banned and suspect sites work and what other options you have, see the [Dealing with Trolls](/tutorials/manage/trolls.html) tutorial.

{% include toc.html %}

## Banned Sites

To configure banned and suspect sites:

1. Select Admin -> Manage.
2. Select "Manage Bans".

You can either ban a specific player (and all their alts), or a site hostname or IP.

### Findsite

The findsite command (help findsite) helps you to find the IP and host of a troublesome player so you can add their site to the banned or suspect lists.

### Partial Matches

Only part of a site needs to match, so listing `verizon.net` would block 123.456.pool.verizon.net and 678.901.pool.verizon.net and so forth.  

{% note %}
This is a 'contains' search, so wildcards (like \*) are not supported.
Be wary of making the match *too* broad.  You don't want to block an entire region of the country.
{% endnote %}

## Banning Proxy Sites

To enable the proxy site ban, set `ban_proxies` to true.  

{% note %}
Enabling this feature requires either a game restart, or a coder character doing `ruby Login.update_blacklist` to initialize the proxy blacklist.  After the initial load, it will be periodically updated.
{% endnote %}

## max_connections

Limits the number of simultaneous connections from a single host/IP.