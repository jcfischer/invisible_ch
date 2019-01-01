---
author: Jens-Christian Fischer
categories: ["musings"]
comments: true
date: 2006-03-08 22:46:02+00:00
layout: post
link: https://invisible.ch/2006/03/08/its-the-cables-stupid/
slug: its-the-cables-stupid
tags: ["blog"]
title: It's the cables, stupid
type: post
wordpress_id: 522
---

Improving my datacenter in the basement, I installed a proper Firewall instead of the dinky 4-port NAT router that connected our house to the wild intranet. I used an [Astaro][1] Security Linux on an old PC, a setup that has served me well in the Office network. To make everything look really good, I used red and green network cables that I had salvaged from somewhere.

![](https://static.flickr.com/40/88652740_3c1c90bc85_t.jpg)Installing the firewall was straightforward, I copied the settings I use at the office and just changed from PPPoE (ADSL) to Ethernet Interface (Cablecom) and was set, more or less. 

Soon after we had internet and I continued to work. But - something didn't seem right. I had intermediate problems, time-outs, drops of connections. *MTU* size, I thought, having seen similar symptoms a couple of years ago. So I switched from 1500 to 1492 to 1400 back to 1500. No joy, as Jerry Pournelle would have said.

I said to myself (and to anybody who would listen): it feels like a loose cable. 

And finally my friend Paul said: Have you tried switching the cables? Then it dawned on me: Those fancy colored cables... I replaced them, rebooted Firewall and Cablemodem for good measure, and lo and behold - all back to normal.

The cables are in the trash. Always check the simple things first.

[1]: https://www.astaro.de


Technorati Tags: [cablecom](https://www.technorati.com/tag/cablecom), [firewall](https://www.technorati.com/tag/firewall), [network](https://www.technorati.com/tag/network), [cables](https://www.technorati.com/tag/cables)
