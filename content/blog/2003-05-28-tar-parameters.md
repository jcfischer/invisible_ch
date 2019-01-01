---
author: Jens-Christian Fischer
categories: ["musings"]
comments: true
date: 2003-05-28 10:53:46+00:00
layout: post
link: http://blog.invisible.ch/2003/05/28/tar-parameters/
slug: tar-parameters
tags: ["blog"]
title: TAR parameters
type: post
wordpress_id: 98
---

This [list of TAR parameters](http://vowe.net/archives/003353.html) comes in really handy.... thanks [vowe](http://vowe.net)
<!-- more -->
tar.gz -> -xvzf 
tar.bz2 -> -xvjf
tar -> -xvf

To create some archives, just replace the 'x' with a 'c' and add the files you want to pack as additional parameters  So 'tar -cvjf mytar.tar.bz2 whatever/' will create a file named mytar.tar.bz2, containing all the files and subdirs below (and including) the directory 'whatever'.
