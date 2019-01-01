---
author: Jens-Christian Fischer
categories: ["musings"]
comments: true
date: 2003-05-05 10:49:41+00:00
layout: post
link: http://invisible.ch/2003/05/05/one-date-down-more-to-go/
slug: one-date-down-more-to-go
tags: ["blog"]
title: One date down - more to go
type: post
wordpress_id: 64
---

I've been quiet the last few days, I know. My time has been unevenly split between work and family (and guess which part got more of my time...) I've had the most unnerving experience yesterday when I moved my Domino application from my development server to the production cluster (two domino servers). 

My tests all ran. Everything looked the way it should. I was happy. Getting up at 3:30 in the morning was worth it - or so I thought...

Then my customer called. Angry. The layout of the menus was all wrong, and if that minor thing was wrong she said, god knows what else would be wrong too. I looked at my browser - all OK. I had her on the phone - and her version was all screwed up. Great. Fucking great. 

I remembered that the production version was running on a cluster. I tried to find differences between the two databases on the two servers. None. Well - one - a document thought missing had turned up on my customers version - not on mine. Stranger and stranger.

Fired of an email to the Notes admin late at night. Agreed to come in at 8 to try and fix the problem.

When I got there I met one angry notes admin. The databases were perfectly in sync - and clearly my problems were not her problems... Ahh

I plugged in and after a nights sleep found the problem with the menus: two views with identical names. The sort order was different on each database. Pure chance, which server would serve the requests. Deleting the views. Replacing the design. All done - fixed.

Domino is great - but sometimes the problems with it can be - shall we say - taxing?

Back to work at my other client. There my login no longer works. Somebody forgot to tell the ID-office about my contract which had been extended. Waiting. Time to write in the blog.
