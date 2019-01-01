---
author: Jens-Christian Fischer
categories: ["musings"]
comments: true
date: 2003-12-01 20:57:08+00:00
layout: post
link: http://blog.invisible.ch/2003/12/01/backuppc-installed/
slug: backuppc-installed
tags: ["blog"]
title: BackupPC installed
type: post
wordpress_id: 210
---

I had a go at installing [BackupPC](http://backuppc.sourceforge.net/) on a smallish personal server I built for a project that didn't take off. The machine is a Via Eden board (with a high-performance C3 500 Mhz CPU :-) ) and a 120 Gig Harddrive. There's a Debian Woody installed and I used this lazy afternoon to convert it to my home server. It already has 40 Gigs of my music and now it's backing up 30 Gigs of data from this laptop.

Setup of BackupPC was somewhat involved and I'm not 100% sure I got it working in the most secure way. Specifically the Apache / CGI / mod_perl side seems to be "not quite right" and would probably fail a Pen-Test. But it works, this machine is being backed up as we speak (wonder how long it's going to take ) and I have a big Todo Item of my chest...
