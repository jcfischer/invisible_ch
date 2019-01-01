---
author: Jens-Christian Fischer
categories: ["musings"]
comments: true
date: 2012-09-10 11:04:09+00:00
layout: post
link: http://blog.invisible.ch/2012/09/10/stuck-with-read-only-sd-card-on-mac/
slug: stuck-with-read-only-sd-card-on-mac
tags: ["blog"]
title: Stuck with read-only SD card on Mac
type: post
wordpress_id: 12068
---

I was trying to use my Mac to format a 16GB SD card with the unix tool 'dd', but I got a 'permission denied' error when trying to write to it - even as root (using sudo). Examining the SD card, the write lock switch was in the correct position, but the DiskUtil tool showed that the card was read only. Weird. Some trawling the Interwebs led to the usual "plz halp me - U good" crap that is all over the forums, but also [this](https://discussions.apple.com/thread/2166984?start=0&tstart=0) forum discussion on the Apple Support forums.

The solution? It seems that the SD reader on the MacBook Pro is a finicky little fellow. Slide the "write lock slider" on the SD card in the middle between locked/unlocked and insert it. Then the card is in read/write mode.


