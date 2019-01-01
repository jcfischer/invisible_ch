---
author: Jens-Christian Fischer
categories: ["musings"]
comments: true
date: 2010-11-22 16:47:59+00:00
layout: post
link: https://invisible.ch/2010/11/22/daily-log-2010-11-22-passenger-3-iui-and-authenticity-tokens/
slug: daily-log-2010-11-22-passenger-3-iui-and-authenticity-tokens
tags: ["blog"]
title: Daily-Log, 2010-11-22, Passenger 3, iUI and authenticity tokens
type: post
wordpress_id: 882
---

An update of our production server to [Passenger 3.0](https://www.modrails.com/) worked without problem - kudos to the guys at Phusion! We have changed several parameters and expect our large Rails apps to run faster and better. The main change was that we keep one passenger running for the most used apps, regardless if the app has been idle or not.

We've had an iPhone layout for [StellenAnzeiger](https://stellenanzeiger.ch) for a long time. Intermittently we got Rails "Invalid AuthenticityToken" errors but were never able to pin them down. Of course, when we tested it, it "just worked (tm)". We had a breakthrough today, when we noticed that the authenticity token we received on the server had spaces in it. It turns out, that the [iUI framework](https://code.google.com/p/iui/) we are using for the iPhone like layout changes "+" to " " in input fields. The authenticity token can contain pluses, so iUI mangled it - and the server promptly complained. The fix is a [one line patch to iui.js](https://code.google.com/p/iui/issues/detail?id=58) - we weren't the first people to run into the problem...
