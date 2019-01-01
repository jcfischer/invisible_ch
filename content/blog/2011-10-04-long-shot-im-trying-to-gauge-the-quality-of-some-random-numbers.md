---
author: Jens-Christian Fischer
categories: ["musings"]
comments: true
date: 2011-10-04 23:56:55+00:00
layout: post
link: http://invisible.ch/2011/10/04/long-shot-im-trying-to-gauge-the-quality-of-some-random-numbers/
slug: long-shot-im-trying-to-gauge-the-quality-of-some-random-numbers
tags: ["blog"]
title: 'Long shot: I''m trying to gauge the quality of some "random" numbers...'
type: post
wordpress_id: 925
---

Long shot: I'm trying to gauge the quality of some "random" numbers that I have generated. I'm using the "dieharder" [http://www.phy.duke.edu/~rgb/General/dieharder.php](http://www.phy.duke.edu/~rgb/General/dieharder.php) library to analyse the data I have (in a file)  
  
I use a file for my data (even though that's not recommended) and give that data to dieharder:  
  
dieharder -g 202 -f my_data.input -s 1  
  
(where -g 202 tells dieharder to use the input file) and -s 1 is the test to run.  
  
This fails spectacularly with all tests. If I create a file of random numbers from one of the built in generators, I get the same (failing) result. Running dieharder with the -v 1 option (for debug purposes), I can see the file of data being read and parsed seemingly correctly.  
  
Any ideas out there in G+ land?


												

**Embedded Link**


												


													![](http://images0-focus-opensocial.googleusercontent.com/gadgets/proxy?container=focus&gadget=a&resize_h=100&url=http%3A%2F%2Fwww.phy.duke.edu%2F%7Ergb%2Fimages%2Frgb_thumbnail.jpg)
												


												[Robert G. Brown's General Tools Pagergb's Books](http://www.phy.duke.edu/~rgb/General/dieharder.php)  

												Robert G. Brown's General Tools Page. Things on the site itself that may be of interest to students or philosophers of any age or generation include complete online books of poetry, various suppor...  

										


										

**Google+:** [View post on Google+](https://plus.google.com/109789939743085010576/posts/FJm46uhJk3S)

  
  
_Post imported by Google+Blog.  Created By [Daniel Treadwell](http://minimali.se/)._
