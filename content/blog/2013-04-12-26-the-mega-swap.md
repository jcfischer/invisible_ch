---
author: Jens-Christian Fischer
categories: ["musings"]
comments: true
date: 2013-04-12 21:48:30+00:00
layout: post
link: https://invisible.ch/2013/04/12/26-the-mega-swap/
slug: 26-the-mega-swap
tags: ["blog"]
title: 26 - the mega swap
type: post
wordpress_id: 12827
---

Today my computer alerted me to no more room on the main disk - strange, because there were over 140 GB free. I fired up Activity Monitor to check for disk and memory and lo and behold - something was very very wrong...

[![Screen Shot 2013-04-12 at 13.36.00](/wp-content/uploads/2013/04/Screen-Shot-2013-04-12-at-13.36.00-300x244.png)](/wp-content/uploads/2013/04/Screen-Shot-2013-04-12-at-13.36.00.png)No idea what UserEventAgent was doing - I forgot to check for which files it had open but 50GB of virtual memory seems just a bit excessive...

Killing the process returned Swap levels to "normal" 11 GB...

Does anyone have an idea what happened here?


