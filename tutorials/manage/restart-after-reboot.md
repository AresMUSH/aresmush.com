---
title: Restart After Reboot
description: 
layout: page
tags:
- manage
- restart
- reboot
---

You'll want to make sure that your game restarts if the server is ever rebooted. 

If you followed the install tutorial on DigitalOcean, the install script should do that for you automatically.

If not, the exact instructions will vary depending on your machine's operating system. Please consult your system documentation for details, but the info here might help.

## Ubuntu

You need to run bin/startares from the aresmush directory **as the ares user**.

The standard install does this with three files.

/root/onboot.sh:

    sudo -u ares -i '/home/ares/onboot.sh'
    
/home/ares/onboot.sh:

    cd aresmush
    bin/startares&

/etc/rc.local:

    /root/onboot.sh &
    exit 0