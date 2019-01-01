---
author: Jens-Christian Fischer
categories: ["musings"]
comments: true
date: 2004-02-26 16:59:10+00:00
layout: post
link: http://invisible.ch/2004/02/26/finding-side-effects-with-idea/
slug: finding-side-effects-with-idea
tags: ["blog"]
title: Finding side effects with IDEA
type: post
wordpress_id: 254
---

I was on a bug hunt the last couple of hours. When I looked at a web page served by our application server, it's content showed up. When I pressed reload, only the summary of the content showed up. Somehow, someone changed my ( my! ) private variable somewhere. I sprinkeld the code liberally with print statements (ahh - nothing goes over a good dose of those) because the app would be quite cumbersome to run in the debugger.

Nada - I could see that the second time, the content size was reduced to a couple of bytes. But no clue who did that to me.

After some consideration, I decided to look at the code again. And [IDEA](http://www.intellij.com) helped me spot the problem in 30 seconds: 

Place the cursor on any expression (in this case on the name of my private variable that got changes). Press CTRL-SHIFT-F7 and all occurences of that expression are highlighted in the editor. Scroll down, take a look and voila: there it was, an assignment to the variable in the wrong function.

![idea-f7.gif](/images/idea-f7.gif)

As it always is: Good tools are a real asset!
