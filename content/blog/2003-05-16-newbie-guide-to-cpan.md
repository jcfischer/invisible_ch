---
author: Jens-Christian Fischer
categories: ["musings"]
comments: true
date: 2003-05-16 10:38:46+00:00
layout: post
link: http://blog.invisible.ch/2003/05/16/newbie-guide-to-cpan/
slug: newbie-guide-to-cpan
tags: ["blog"]
title: Newbie Guide to CPAN
type: post
wordpress_id: 75
---

In my current project I have the pleasure (?) to work with Perl. I found out that there are hundres (thousands?) of useful modules out there. Before they can be used however, they have to be downloaded an installed... Grief!

Here's the dummies guide to doing it: (Assuming a [Cygwin](http://www.cygwin.com) installation on a Win32 box)
<!-- more -->




  1. Locate the module on [Cpan](http://www.cpan.org)


  2. Download the module.


  3. You have a _module-version.tar.gz.tar_ file which is useless (or so it seems)


  4. mv module-version.tar.gz.tar module-version.tar.gz

. This removes the extra .tar extension...


  5. gzip -dc module-version.tar.gz | tar -xof -

. This extracts the module and creates a directory called "module-version"


  6. In that directory:

    
    
    perl Makefile.PL
    make
    make test
    make install
    



  7. Now you should have the module installed and running



Thanks to [the Install FAQ](http://www.cpan.org/modules/INSTALL.html)
