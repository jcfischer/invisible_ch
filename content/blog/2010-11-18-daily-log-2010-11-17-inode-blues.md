---
author: Jens-Christian Fischer
categories: ["musings"]
comments: true
date: 2010-11-18 06:55:31+00:00
layout: post
link: http://blog.invisible.ch/2010/11/18/daily-log-2010-11-17-inode-blues/
slug: daily-log-2010-11-17-inode-blues
tags: ["blog"]
title: Daily Log, 2010-11-17, inode blues
type: post
wordpress_id: 879
---

A few weeks ago we upgraded the RAM on our main server. At that point, I discovered that the external backup drive we use to backup our hosting users home directory was full and no data could be written to it. I never discovered the problem, because `df -h` always told me that there was plenty of space left. However when I tried to create a file on the drive, I got a 
`
    
    
    touch /backup/bla
    touch: cannot touch `/backup/bla': No space left on device
    

`
error.
I suspected that we had run out of inodes, but hadn't yet seen that situation before so I didn't know what to look for. A bit of googling led me to the post: [No space left on device - running out of inodes](http://www.ivankuznetsov.com/2010/02/no-space-left-on-device-running-out-of-inodes.html). A quick `df -i` showed me indeed that there were no inodes left on the backup device.

Unfortunately I couldn't just follow the suggestion of Ivan and delete small files. We use [rsnapshot](http://rsnapshot.org/) for backups  - and that creates a lot of small files (namely the links between the different backup sets). The only solution thus is to create more inodes when the filesystem is generated. Our 256 GB backup disk has 16 million inodes. I'll try with some more millions next, that should be enough...

I created a new iscsi backup disk on our dedicated backup device (a Synology 209+) and created the filesystem with the following magic incantation:

`
    
    
    mkfs.ext3 -b 1024 -i 1024 /dev/sdd1
    

`

I chose a smaller blocksize (1024 instead of 4096 bytes) due to the fact, that the disk will mostly store symlinks. As they only are a few bytes long, 1024 byte blocks should give us better usage of the disk. Also I dropped the number of bytes per inode to 1024 - all in all that gives us over 268 million inodes - should be enough for quite a while...

