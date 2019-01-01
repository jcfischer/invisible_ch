---
author: Jens-Christian Fischer
categories: ["musings"]
comments: true
date: 2008-04-12 22:12:07+00:00
layout: post
link: https://invisible.ch/2008/04/12/shell-meme/
slug: shell-meme
tags: ["blog"]
title: Shell Meme
type: post
wordpress_id: 658
---

I [did this before][1]...

    jcf@Arwen:amazon: history|awk '{a[$2]++} END{for(i in a){printf "%5d\t%s\n ",a[i],i}}'|sort -rn|head
       191	git
        58	rake
        48	cd
        40	cap
        25	mate
        24	jruby
        16	ruby
        10	ssh
         7	script/plugin
         6	rm


[1]: /2006/09/28/one-of-theses-memes/
