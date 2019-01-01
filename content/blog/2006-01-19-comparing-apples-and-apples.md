---
author: Jens-Christian Fischer
categories: ["musings"]
comments: true
date: 2006-01-19 16:03:09+00:00
layout: post
link: http://blog.invisible.ch/2006/01/19/comparing-apples-and-apples/
slug: comparing-apples-and-apples
tags: ["blog"]
title: Comparing Apples and... Apples?
type: post
wordpress_id: 505
---

Macworld has a [performance test of the new dual core iMac vs. the old G5 iMac][1]. They are saying, that the new Dual Core iMacs don't perform twice as fast, and seem quite a bit disappointed.

I think, they just aren't comparing Apples to Apples. Let me explain:

The old iMac is a single processor G5. The new iMac a Dual Core Intel chip. The applications they are testing (iMovie, iPhoto, iTunes, creating a ZIP file, iDVD and BBEdit) are *most likely* (correct me if I'm wrong, please) single threaded applications. That means, that the raw work of converting, compressing, searching and whatnot is running on a single core. Only applications that are built to be multi-threaded would be able to share the work on both cores. So what the test results are showing us (imo) is that the Intel Dual Core processor *running an application on basically one of it's core* is a wee bit faster than the G5.

Now that's not a mean feat for Intel, because it shows, that the Yonah core is as fast a processor as the G5. 

Somebody please repeat these tests with the following setup:

* Dual G5 PowerMac vs. Intel iMac Dual Core
* Quad G5 PowerMac vs. Intel iMac Dual Core

and the following new tests

* A program that actually uses multiple threads to do the work (I don't know of any, but I'd imagine any graphics rendering program worth it's salt is able to parallelize it's workload on multiple processors)
* Starting both an iTunes and an iMovie task on a G5 iMac vs. the Intel iMac

I think only then are we really comparing Apples to Apples

PS: If somebody sends me the necessary Hardware, I'd do the tests myself


[1]: http://www.macworld.com/2006/01/features/imaclabtest1/index.php


Technorati Tags: [apple](http://www.technorati.com/tag/apple), [benchmark](http://www.technorati.com/tag/benchmark), [iMac](http://www.technorati.com/tag/iMac), [intel](http://www.technorati.com/tag/intel), [mac](http://www.technorati.com/tag/mac), [refactoring](http://www.technorati.com/tag/refactoring)
