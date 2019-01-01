---
author: Jens-Christian Fischer
categories: ["musings"]
comments: true
date: 2005-01-17 10:33:34+00:00
layout: post
link: http://blog.invisible.ch/2005/01/17/apache-2-not-coming-up/
slug: apache-2-not-coming-up
tags: ["blog"]
title: Apache 2 not coming up?
type: post
wordpress_id: 364
---

If you have this: `httpd: could not open document config file /opt/apache2/httpd.conf` when you try to start your Apache 2 with a different config file, then do this:

`/opt/apache2/bin/httpd -f /opt/apache2/conf/httpd.conf`

It looks like Apache doesn't like relative paths when it's called with a different config file.
