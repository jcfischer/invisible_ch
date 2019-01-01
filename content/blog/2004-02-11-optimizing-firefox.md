---
author: Jens-Christian Fischer
categories: ["musings"]
comments: true
date: 2004-02-11 11:33:39+00:00
layout: post
link: http://blog.invisible.ch/2004/02/11/optimizing-firefox/
slug: optimizing-firefox
tags: ["blog"]
title: Optimizing FireFox
type: post
wordpress_id: 248
---

In Mozilla FireFox: type "about:config" in the adressbar and the hunt those settings and change them accordingly:

`
user_pref("general.smoothScroll", true);
user_pref("network.image.imageBehavior", 0);
user_pref("network.http.max-connections", 48);
user_pref("network.http.max-connections-per-server", 16);
user_pref("network.http.pipelining", true);
user_pref("network.http.pipelining.firstrequest", true);
user_pref("network.http.pipelining.maxrequests", 100);
user_pref("network.http.proxy.pipelining", true);
user_pref("nglayout.initialpaint.delay", 100);
`

by [Geek Styke](http://www.farrokhi.net/blog/archives/000235.html) via [Simon](http://simon.incutio.com) and his blogmarks
