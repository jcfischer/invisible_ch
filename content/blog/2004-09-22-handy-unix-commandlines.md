---
author: Jens-Christian Fischer
categories: ["musings"]
comments: true
date: 2004-09-22 13:12:53+00:00
layout: post
link: http://blog.invisible.ch/2004/09/22/handy-unix-commandlines/
slug: handy-unix-commandlines
tags: ["blog"]
title: Handy Unix commandlines
type: post
wordpress_id: 324
---

It's hard to memorize all the fun things you can do with the shell on a *nix system.

Here's my crib-sheet:
**Find all files containing _string_ in the current directory tree**

find . -type f -exec grep string {} \; -print

**In all files in directories dir1 and dir2, replace "aaa" with "bbb"**


    
    #!/bin/sh
    
    for i in `find ./dir1 ./dir2 -type f`; do
        sed -e"s/aaa/bbb/g" $i> $i.$$
        mv $i.$$ $i
    done
    



tbc
