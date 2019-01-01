---
author: Jens-Christian Fischer
categories: ["musings"]
comments: true
date: 2003-04-24 14:07:42+00:00
layout: post
link: http://blog.invisible.ch/2003/04/24/this-site-sped-up/
slug: this-site-sped-up
tags: ["blog"]
title: This site sped up
type: post
wordpress_id: 61
---

Regular visitors know about my problems with the speed of this site. There always was a delay of several seconds for every request made to the webserver (apache).

Thinking out loud with my colleague and friend Matthias led me to play with the configuration of my named deamon. Lo and behold - there was an entry for an unknown DNS server in resolve.conf. Replacing that with 127.0.0.1 for my caching named made all the difference.

**Update:** Dont't forget to restart apache after named
`
/etc/init.d/named restart
/etc/init.d/httpd restart
`
