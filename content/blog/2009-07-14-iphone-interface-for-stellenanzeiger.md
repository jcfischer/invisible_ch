---
author: Jens-Christian Fischer
categories: ["musings"]
comments: true
date: 2009-07-14 21:53:22+00:00
layout: post
link: https://invisible.ch/2009/07/14/iphone-interface-for-stellenanzeiger/
slug: iphone-interface-for-stellenanzeiger
tags: ["blog"]
title: iPhone interface for Stellenanzeiger
type: post
wordpress_id: 741
---

The project we are working on for a job-search box in Switzerland ("[stellenanzeiger.ch](https://stellenanzeiger.ch)") has started nicely and we have already reached the "visitors per month" goal, our client had for the end of the year.
We are constantly applying small fixes, reading more jobs (that would be a blog post all by itself), recognizing duplicates, handling very very weird internet sites etc.
As a "fun" project, [Keith](https://invisible.ch/ueber-uns/team/keith-bingman/) wrote an iPhone web interface for the site: 

![bild-3](/wp-content/uploads/2009/07/bild-3-199x300.png)![bild-5](/wp-content/uploads/2009/07/bild-5-199x300.png)

This side project has been written with the [iUI framework](https://code.google.com/p/iui/) and after a few false starts, has been coming along very nicely.

We have implemented the most basic functionality of the site: searching for a job and will be looking at the number of visitors to determine if we will iPhone enable more pieces of the website. 

We are using the [Rails iPhone Mime-Type](https://www.slashdotdash.net/2007/12/04/iphone-on-rails-creating-an-iphone-optimised-version-of-your-rails-site-using-iui-and-rails-2/) to determine, if a visitor is coming to us with an iPhone or iPod Touch. If there is a special iPhone version for the page he's looking at, we will serve it directly. Personally I think that this is the better way, than having a separate "m" or "iphone" sub-domain. In the first case, you'd have to differentiate all the different mobile browser (and boy are there many and do the vary), in the second case, you'd have to install a sub-domain for every browser type you support.

Better to just figure out what mobile browser the user is coming in with and serving an optimized version if available.
