---
title: Banning with the Firewall
description: 
layout: page
---

While the in-game ban commands will keep someone from connecting to the game and logging in, there are times when you'll need to block someone at the server level. This will prevent them from even _trying_ to connect, or even viewing the public website.

Games installed with the one-click image come with the `ufw` firewall installed. You can also install ufw manually. To block someone in the firewall, execute this command from the server shell:

```
sudo ufw insert 1 deny from BAD_IP_GOES_HERE
```

(the "insert 1" puts the rule above other "allow" rules)

If you aren't sure of the IP, you can use the `findsite` command in-game or check their connections in the debug log. If they are currently connected, you can also use the following command in the server shell to show connections to the game port. Be sure to check both the MU client port (e.g., 4201) and the websocket port (from server.yml - usually 4202).

```
ss -tapn | grep 4201
```