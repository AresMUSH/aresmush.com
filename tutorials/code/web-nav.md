---
title: Web Portal Navigation
description: 
layout: page
tags:
- code
- webportal
---

The Web Portal supports two navigation menus - a sidebar and a top navbar.  These navigation menus are controlled by the following code files:

* `ares-webportal/app/components/global-sidebar.hbs and .js`
* `ares-webportal/app/components/global-navbar.hbs and .js`

{% tip %} 
Always use the Ember link-to helper rather than raw  `<a href>`  tags for internal web portal links.  This is important for maintaining the internal web portal state.  It's also the reason why changing the navbar requires changing the code instead of just a configuration file.
{% endtip %}

The sidebar is driven by the `GetSidebarInfoRequestHandler` web request.  If you want additional data to appear on the sidebar (for example - adding a list of recently-approved characters), you'll need to update that handler.