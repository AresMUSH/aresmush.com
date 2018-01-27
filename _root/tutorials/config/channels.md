---
toc: ~config~ Configuring the Plugins
title: Configuring channels.
---
# Configuring the Channel System

To configure the Channels plugin:

1. Go to the Web Portal's Admin screen.  
2. Select Advanced Config.
3. Edit `channels.yml`

## start_marker and end_marker

You can configure the characters that appears at the beginning and end of the channel name.  This lets you alter the appearance to do things like:

    <Chat> Faraday says, "This is MUSH style."
    [Chat] Faraday says, "This is MUX style."

Start and end markers can include ansi color and other formatting codes.

## default_channels

You can configure which channels new characters join by default when they are first created.  This should be a list.  For example:

    default_channels:
        - Questions
        - Chat