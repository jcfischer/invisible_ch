---
author: Jens-Christian Fischer
categories: ["musings"]
comments: true
date: 2007-03-26 17:10:18+00:00
layout: post
link: http://blog.invisible.ch/2007/03/26/when-tables-are-a-bad-idea/
slug: when-tables-are-a-bad-idea
tags: ["blog"]
title: When tables are a bad idea
type: post
wordpress_id: 615
---

Remember my [plea for help][1] a couple of weeks ago? I haven't really had any success with this (even though nice people tried to help me). 

But then things picked up in the last few days: I browsed through the "Agile Web Development with Rails" book and found a note that basically said, that Internet Explorer is borked when you try to manipulate the DOM of a table. It seems, that it's not able to handle the innerHTML attribute of table rows or table cells.

Then last week, I met [Wolmer Facchin][2] who just jumped into rails and has been doing a lot of DOM / CSS / Semantic HTML work. Today, I described my problem in more detail. After just two hours I got an email from him, telling me about a couple of bugs in my HTML and a suggested fix, using dl lists. Not only has my code gotten easier, I got rid of a large table, and my application now works across all browsers (including IE). Thanks Wolmer!

Oh: Yes, you will be able to see that application... At [Tweakfest][3] at the end of may. 


[1]: http://blog.invisible.ch/2007/02/01/i-could-need-some-help-with-javascript-and-ie-debugging/
[2]: http://cchin.ch
[3]: http://www.tweakfest.ch


Technorati Tags: [css](http://www.technorati.com/tag/css), [ie](http://www.technorati.com/tag/ie), [internet explorer](http://www.technorati.com/tag/internet explorer), [tweakfest07](http://www.technorati.com/tag/tweakfest07), [rails](http://www.technorati.com/tag/rails)
