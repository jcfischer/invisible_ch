---
author: Jens-Christian Fischer
categories: ["musings"]
comments: true
date: 2003-08-06 01:33:05+00:00
layout: post
link: http://invisible.ch/2003/08/06/cpu-pegged-at-100-who-to-blame-part-1/
slug: cpu-pegged-at-100-who-to-blame-part-1
tags: ["blog"]
title: CPU pegged at 100%, Who to blame? (Part 1)
type: post
wordpress_id: 151
---

In preparation for the [project ahead](http://www.invisible.ch/archives/000150.html) I decided to install IIS and the latest fixes on this Windows XP SP1 machine. Then I got [ActiveState Python](http://www.activestate.com/Products/ActivePython/) to work as a handler to .py files (something that [Microsoft Knowledgebase](http://support.microsoft.com/default.aspx?scid=kb%3Ben-us%3B276494) helps you with.

I was rewarded with a working IIS con Python server and an unbelievable slow machine. Bringing up the Task Manager shows my CPU pegged at 100% - but none of the processes running seem to be responsible for it. Firing up ProcessExplorer by [SysInternals](http://www.sysinternals.com/) shows a lot more information about the running processes, but no culprit.

Googling with [this query](http://www.google.com/search?q=xp+sp1+100%25+cpu+no+process&hl=en&lr=&ie=UTF-8&oe=utf-8&start=10&sa=N) brings some interesting reads, but no definitve answer.

It's rebooting madness at the moment. Killing processes to see if they are guilty of eating my CPU, deinstalling XP Fixes (811493), deinstalling IIS - but nothing has helped so far. 

My system is a bit more responsive than when this started, but it takes about three times as long to boot or shutdown. The CPU is still pegged at 100%, the fans on my Inspiron 8200 blow as if there was no tomorrow and I'm without a clue... Has the time come to [reinstall Windows XP in 5 hours](http://diveintomark.org/archives/2003/08/04/xp)? Shudder
