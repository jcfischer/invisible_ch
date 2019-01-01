---
author: Jens-Christian Fischer
categories: ["musings"]
comments: true
date: 2003-03-13 05:49:01+00:00
layout: post
link: http://invisible.ch/2003/03/13/how-to-start-a-linux-server/
slug: how-to-start-a-linux-server
tags: ["blog"]
title: How to start a linux server
type: post
wordpress_id: 30
---

What happens when you have uptime of over 200 days and you need to reboot your linux machine? You forget how to do things. And if you don't have the documententation handy....

Here's how the Notes server on linux is started:

su notes
cd /usr/local/notesdata
/opt/lotus/bin/server

or for a more detailes script, check out [this entry](http://www-10.lotus.com/ldd/46dom.nsf/55c38d716d632d9b8525689b005ba1c0/687c9d1e2100127585256a34006c48cf?OpenDocument&Highlight=0,anthony,barker,password,linux) on [notes.net](http://www.notes.net)
