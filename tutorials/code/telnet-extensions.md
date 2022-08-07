---
title: Telnet Extensions
description: 
layout: page
---

Ares supports basic [Telnet Negotiation](http://mud-dev.wikidot.com/telnet:negotiation) with clients, including:

* `CHARSET` - If a client indicates that it will accept charset commands, Ares will instruct it to set the character set to UTF8.  This allows many clients to auto-negotiate the proper character set without you needing to adjust [manual settings](/clients.html).
* `NAWS` - This allows the client to send AresMUSH information about the client's window size.  You can access this information through `client.window_height` and `client.window_width`. However, the standard Ares code does not make use of this information and is designed for a standard 78-character wide terminal.

## MUD Extensions (MSSP/MCP/GMCP)

Ares does not support [MUD Server Status Protocol (MSSP)](https://tintin.sourceforge.io/protocols/mssp/). It has its own, more robust, game status reporting system used to build the [AresCentral Game Directory](https://arescentral.aresmush.com/), and I do not see a lot of value in supporting MSSP for MUD directories.

Similarly, Ares does not support [MUD Client Protocol (MCP)](https://www.moo.mud.org/mcp/) or [Generic MUD Communication Protocol (GMCP)](https://www.gammon.com.au/gmcp).  Ares is designed for MUSHes, not MUDs, and these protocols are not in widespread use among the MUSH community to the best of my knowledge.  Planned changes to Ares will enable next-gen clients to communicate directly with the game via a standard protocol someday, but it will not be overlaid on telnet as MCP/GMCP are.

If you have a compelling use case where you need these extensions, feel free to provide [feedback](/feedback.html) and it will be considered.