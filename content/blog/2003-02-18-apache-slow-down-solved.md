---
author: Jens-Christian Fischer
categories: ["musings"]
comments: true
date: 2003-02-18 00:36:47+00:00
layout: post
link: http://invisible.ch/2003/02/18/apache-slow-down-solved/
slug: apache-slow-down-solved
tags: ["blog"]
title: Apache slow down solved?
type: post
wordpress_id: 2
---

It seems that something with my dynamic execution of cgi's causes the slowdown on Apache. Now that the Blog is static, everything seems to move quite fast (except for the fact that it takes me ages to edit the pages  - but hey - that's ok, isn't it?)

Check out a slow apache server on: [My old Blog done with PikiePikie](http://www.invisible.ch/cgi-bin/pikie) (of course that link now is broken - hmmm)

The link doesn't work anymore? Though - it turns out that either Python or the Python Apache handler or god knows what else was the culprit... This site is now as fast as it can be ;-)

Actually - the real reason can be found here: [This Site Sped up](http://www.invisible.ch/archives/000061.html)... Check your resolv.conf...
