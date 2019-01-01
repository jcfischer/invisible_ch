---
author: Jens-Christian Fischer
categories: ["musings"]
comments: true
date: 2009-03-16 21:03:46+00:00
layout: post
link: https://invisible.ch/2009/03/16/scaling-twurli/
slug: scaling-twurli
tags: ["blog"]
title: scaling twurli
type: post
wordpress_id: 701
---

[twu.li](https://twur.li) starts to grow. We track almost 8000 twitterers for their updates and collect the URLs. This takes more and more time (there is quite some potential for optimizing it by requesting things in parallel). Right now, that's about 3 hours to do a full scan (and it will get worse). New URLs can therfore show up with quite a delay. To alleviate that, we implemented a simple priority queue system. The result? The more URLs someone tweets, the more often we will read your timeline. Tweeting less drops the priority for this user and we will use longer intervals. So twitterers like [timoreilly](https://twur.li/timoreilly) will get scanned more often than the huge bulk, that doesn't tweet as often.

One more step to make twur.li really useful.
