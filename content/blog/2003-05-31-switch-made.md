---
author: Jens-Christian Fischer
categories: ["musings"]
comments: true
date: 2003-05-31 13:13:53+00:00
layout: post
link: http://blog.invisible.ch/2003/05/31/switch-made/
slug: switch-made
tags: ["blog"]
title: Switch made
type: post
wordpress_id: 105
---

It worked ;-)
I had to fumble a bit to get LILO to work with my harddisks, but I found a [helpful description](http://www.linuxtag.org/cgi-bin/yabb/YaBB.pl?board=knoppix-de;action=display;num=1045345401;start=3) over on the [Knoppix  Formums](http://www.linuxtag.org/cgi-bin/yabb/YaBB.pl) that did the trick for me...

More small things that needed fixing:


  * Can't access my other harddisk as non-root


Fixed:

  * sound is garbled in hd-install, works fine when booting Knoppix from CD  
add "alsa" to the linux kernels boot options
