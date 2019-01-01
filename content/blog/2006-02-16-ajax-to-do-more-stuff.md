---
author: Jens-Christian Fischer
categories: ["musings"]
comments: true
date: 2006-02-16 06:49:32+00:00
layout: post
link: http://blog.invisible.ch/2006/02/16/ajax-to-do-more-stuff/
slug: ajax-to-do-more-stuff
tags: ["blog"]
title: Ajax to do more stuff?
type: post
wordpress_id: 514
---

Tim Bray over at Ongoing talks about [AJAX Performance][1]. His point being, that we should use AJAX to offload heavy computation from the web-server to the users browser. 

> I suspect there's a huge system-wide optimization waiting out there for us to grab, by pushing as much of the templating and page generation work out there onto the clients. In particular, when you're personalizing a page, assign all the work you can to the personal computer sitting in front of the person in question.

That sounds like a really interesting idea. In my Rails applications I see a lot of time spent in the renderer, not in the database portion. Maybe something to look at, when I get back from the mountains...

[![](http://static.flickr.com/25/99713878_71c5054bcf_m.jpg)](http://www.flickr.com/photos/jcfischer/99713878/)


[1]: http://www.tbray.org/ongoing/When/200x/2006/02/14/AJAX-Performance


Technorati Tags: [ajax](http://www.technorati.com/tag/ajax), [performance](http://www.technorati.com/tag/performance), [rubyonrails](http://www.technorati.com/tag/rubyonrails)
