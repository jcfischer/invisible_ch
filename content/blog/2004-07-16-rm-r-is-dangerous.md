---
author: Jens-Christian Fischer
categories: ["musings"]
comments: true
date: 2004-07-16 10:58:59+00:00
layout: post
link: http://blog.invisible.ch/2004/07/16/rm-r-is-dangerous/
slug: rm-r-is-dangerous
tags: ["blog"]
title: rm -r is dangerous
type: post
wordpress_id: 299
---

Uh oh.

Executing rm -r with root permission is dangerous (as others, unnamed persons know). Luckily not in / and not on a production server.

Learn this lesson: When testing scripts that delete files, do an echo instead of a rm until you are sure, that you are in the right path.

Waiting for the restore crew...

**Update:** The directory is back - time to leave for the weekend, I guess.
