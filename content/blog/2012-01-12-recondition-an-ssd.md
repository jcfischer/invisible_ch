---
author: Jens-Christian Fischer
categories: ["musings"]
comments: true
date: 2012-01-12 12:34:41+00:00
layout: post
link: http://invisible.ch/2012/01/12/recondition-an-ssd/
slug: recondition-an-ssd
tags: ["blog"]
title: Recondition an SSD
type: post
wordpress_id: 11542
---

Yesterday I read the article by Patrick Lenz about his [experiences with an external SSD on his iMac](http://patricklenz.com/posts/an-external-ssd-to-boot-my-imac). This prompted me to investigate the speed of my MacBook Pros SSD with [Black Magic DiskSpeed](http://itunes.apple.com/us/app/blackmagic-disk-speed-test/id425264550?mt=12). Instead of 100 MB/s write speed, I saw a low of 14 MB/s for writing to disks. Searching a bit around led me to the article about [SSD Reconditioning](http://macperformanceguide.com/Storage-SSD-Reconditioning.html) which recommended overwriting the disk with empty data multiple times.

I had thought about the same thing after having enabled TRIM Support on Mac OSX Lion with [TRIM enabler](http://www.groths.org/?p=562). I only had a couple Gigabytes free on my 240GB SSD so I doubted that enabling TRIM after almost a year of operations would do much good. I had always put off the act of cloning, deleting and re-cloning my disk, but the write speed I saw was so abysmal (plus I had seen a lot of recent slow downs of my MBP) that I decided to just do it.

I cloned my internal SSD to an external Disk with [SuperDuper](http://www.shirt-pocket.com/SuperDuper/SuperDuperDescription.html) (a process of several hours), and then booted of it. Then I used DiskUtility to delete the internal SSD. The article on reconditioning recommends the DiskTester tools to run a "recondition" command, so I did. It showed me average write speeds of 250 MB/s -- the SSD nominal speed. I didn't complete a full reconditioning (filling the disk 4 times in a row), because I suspect that deleting the disk with TRIM enabled is enough to tell the SSD disk controller that the disk is empty. Finally I cloned the external disk back onto the internal SSD and hey presto - my write speed is up to around 100MB/s and reads around 180MB/s.

The whole computer feels like new again.

Things to note:

I had full disk encryption enabled before, and I haven't now, so parts of the speed up might be related to that. I will re-enable encryption in a week or so, and see how the speed changes.

Also, SuperDuper took several attempts (in both directions) to clone the disk. It failed 2 times, and once locked up the computer completely. Thankfully one can just run SuperDuper again, and it will pick up where it (was) stopped. It's still an unnerving feeling when that happens - but it seems that I have everything that I should have. (The other unnerving thing is the fact, that I now have around 20 GB more space on my disk than before. I wonder what wasn't copied when I made the backups...)
