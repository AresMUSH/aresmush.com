---
title: Transferring a Game
description: 
layout: page
tags:
- management
---

Before transferring a game to new ownership, you should consider that players have entrusted the current admins, not necessarily the new ones, with all data they have stored on the game. Private and/or sensitive data can include:

- Email Address (if set)
- Handle Preferences
- Mail
- Pages/PMs
- Unshared Scenes
- IP/Hostname

{% note %}
The above list is not all-inclusive, especially if you have custom code or plugins installed. As a game runner, you are responsible for compliance with any local/regional laws concerning the handling and transfer of private data.
{% endnote %} 

The following code can be run using [tinker](/tutorials/code/tinker.html) to wipe the bulk of sensitive data from the game prior to a transfer.

{% tip %}
Give the players plenty of warning before doing this, so they can back up whatever they need to.
{% endtip %}

```
Character.all.each do |char|
  char.delete_pages
  char.delete_mail
  AresCentral.unlink_handle(char)
  char.wipe_login_data(false)
end

Scene.all.select { |s| s.completed && !s.shared }.each do |scene|
  scene.delete
end    
```

The above code does not wipe IP address, because it has value to admin both for security and character recovery (forgotten passwords). Should you wish to clear that too, just change the `wipe_login_data` call from false to true. Players who don't wish their IPs to be transferred can always log in from public wifi or a VPN to obfuscate their IP prior to the transfer.