---
author: Jens-Christian Fischer
categories: ["musings"]
comments: true
date: 2006-09-28 21:53:00+00:00
layout: post
link: http://invisible.ch/2006/09/28/one-of-theses-memes/
slug: one-of-theses-memes
tags: ["blog"]
title: One of theses memes
type: post
wordpress_id: 560
---

Straight from my shell

    $ history|awk '{print $2}'|awk 'BEGIN {FS="|"} {print $1}'|sort|uniq -c|sort -rn|head -10
     121 rake
      71 cd
      49 ruby
      29 ls
      24 mongrel_rails
      23 tail
      21 svn
      16 mate
      15 sudo
      15 ps

via [Anarchaia][1]

[1]: http://anarchaia.org/archive/2006/09/28.html


Technorati Tags: [meme](http://www.technorati.com/tag/meme), [shell](http://www.technorati.com/tag/shell), [unix](http://www.technorati.com/tag/unix)
