---
author: Jens-Christian Fischer
categories: ["musings"]
comments: true
date: 2005-05-13 12:47:28+00:00
layout: post
link: http://blog.invisible.ch/2005/05/13/to-synchronize-or-not/
slug: to-synchronize-or-not
tags: ["blog"]
title: To synchronize or not
type: post
wordpress_id: 409
---


The tale of the joys of asynchronous vs. synchronous processing.



In one of my application users edit rich text in a web browser. This has been working well for 2 years, but all of a sudden problems have appeared. When the users edit very large portions of text, it sometimes is cut off at an arbitrary position. Time do do some debugging...


<blockquote>
**Insert:** One thing I like about my job in IT - and I mean really like - is the fact, that all strange behavior can be traced back to a cause. The cause may be hidden, it may be beneath several level of seemingly wrong things (that turn out to be correct) but it's there. Always. It may take some time to find it, but I have found each and everyone in the past. 
  
This fact gives me a lot of confidence and my clients hear "that's the way it is, and I can't solve it" a lot less than earlier in my career.
</blockquote>


To make things worse, this was working sometimes and failing sometimes. Things don't happen at random in a computer, and if they do, then the obvious suspicion is that there is a timing issue.



In my application, I do the rich-text editing in a pop up window. I use an ActiveX based editor control that takes a couple of seconds to load, and I didn't want to put that burden on the user every time he just edits some meta data. The pop-up window transfers the text content to the main window when the users presses save and then triggers the **submit()** action on the main form, and then reloading the main window. I was using Javascript timers to do that:




  * calling the submit


  * waiting 5 seconds before triggering the reload


  * waiting another 0.5 seconds before closing the pop-up window


  * 



You of course already know the problem: The save took longer than the allocated 5 seconds, and the reload caused the browser to reload the old values, leading to the truncation. Changing the way the application handles this case (synchronizing the save and the reload) took care of this problem

