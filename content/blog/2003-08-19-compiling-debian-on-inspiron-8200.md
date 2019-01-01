---
author: Jens-Christian Fischer
categories: ["musings"]
comments: true
date: 2003-08-19 23:24:24+00:00
layout: post
link: https://invisible.ch/2003/08/19/compiling-debian-on-inspiron-8200/
slug: compiling-debian-on-inspiron-8200
tags: ["blog"]
title: Compiling Debian on Inspiron 8200
type: post
wordpress_id: 166
---

I installed Woody (the "stale" release) on my Inspiron 8200 and followed both the link mentioned below and [Stephan Wehrheims Instructions](https://www.stephanwehrheim.de/computer/dell8200+debian30/dell8200+debian30.html) and got a running system fairly soon. After compiling the kernel (and flipping options rand^h^h^h^h with care and deliberation) I was left with a kernel that booted but didn't have network connection. The ping command claimed: sendto: Network not reachable. Digging around on Google convinced me that my kernel compilation experiments had gone astray. After some consultation with working .config files, I ended up with this file:
    
    /usr/src/linux/<a href="https://www.invisible.ch/debian/.config">.config</a>

that gives me a booting kernel that has network support.
