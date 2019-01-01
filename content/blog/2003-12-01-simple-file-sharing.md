---
author: Jens-Christian Fischer
categories: ["musings"]
comments: true
date: 2003-12-01 23:52:27+00:00
layout: post
link: http://blog.invisible.ch/2003/12/01/simple-file-sharing/
slug: simple-file-sharing
tags: ["blog"]
title: Simple File Sharing
type: post
wordpress_id: 213
---

The first backup with [BackupPC](http://backuppc.sourceforge.net) has finished - faster than I expected. When I checked the backup set, I saw, that the /Windows and /Documents and Settings directories didn't get backed up....

Hmm - looking at their properties, I found that there were not shareable because "the operating system needs them"...

What? 

A bit of searching on the mailinglist of BackupPC found someone with a [similar problem](http://sourceforge.net/mailarchive/forum.php?thread_id=2901188&forum_id=503) and with the solution: There's a "simple sharing" option in Windows XP - a dumbed down version so to speak. Switching it off is described in the [MS Knowledgebase](http://support.microsoft.com/?kbid=304040%3E).

Always learning, are we!
