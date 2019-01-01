---
author: Jens-Christian Fischer
categories: ["musings"]
comments: true
date: 2003-03-19 23:03:26+00:00
layout: post
link: http://invisible.ch/2003/03/19/ie-6-ie6-from-old-blog/
slug: ie-6-ie6-from-old-blog
tags: ["blog"]
title: IE 6 != IE6 (from old blog)
type: post
wordpress_id: 36
---

What's the difference between IE6.2800 on WindowsXP SP1 and IE6.2600 on Windows2000? 6 hours of finding a workaround for what seems to be a bug in IE6 on Win2000. In the application I'm writing I had to edit richt-text (using [eWepEditPro](http://www.ektron.com/)). I did that in a child window and triggered a saveAndReload function in the main document. (Because I'm working with a Domino backend - things have to be saved from time to time ;-) Anyway - on my machine it worked. On my customers machine, the trigger of the function in the parent document didn't work (window.opener.saveAndReload(); ). Spent hours figuring out where the problem was. Another couple of hours spent to find a workaround that works on both machines and gives me the same functionality. 

It works now... Doing a fix-priced project has it's drawbacks...
