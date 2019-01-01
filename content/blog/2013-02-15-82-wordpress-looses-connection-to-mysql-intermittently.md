---
author: Jens-Christian Fischer
categories: ["musings"]
comments: true
date: 2013-02-15 17:10:20+00:00
layout: post
link: https://invisible.ch/2013/02/15/82-wordpress-looses-connection-to-mysql-intermittently/
slug: 82-wordpress-looses-connection-to-mysql-intermittently
tags: ["blog"]
title: 82 - Wordpress looses connection to MySql intermittently
type: post
wordpress_id: 12174
---

This is more a plea for help than a real blog post.

Those of you that visit this blog with a browser might have seen the "Database connection error" page instead of the content. Usually, a simple reload takes care of the problem, and the you can read my ramblings. However this is annoying. More annoying, that I have exactly the same problem on another server with the same setup. Both servers are stock [Joyent Smartmachines](https://joyent.com/products) (small ones). Nothing special is configured on them, I have used the Webmin tools to configure the domains, setup the database and uploaded the Wordpress folders.

The database configuration per se is OK (otherwise I wouldn't be posting this and you wouldn't be reading it). The search on the interwebs has turned up the usual bunch of clueless people on the forums and sadly nothing on Stackoverflow or Serverfault.

Has anyone got a clue on where I might look for a solution to this?

    
    #mysql -V
    mysql Ver 14.14 Distrib 5.5.16, for solaris11 (i386) using readline 6.2



    
    # php -v
    PHP 5.3.8 (cli) (built: Dec 6 2011 20:23:50) 
    Copyright (c) 1997-2011 The PHP Group
    Zend Engine v2.3.0, Copyright (c) 1998-2011 Zend Technologies



    
    # httpd -v
    Server version: Apache/2.2.21 (Unix)
    Server built: Dec 6 2011 20:59:33
