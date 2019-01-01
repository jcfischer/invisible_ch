---
author: Jens-Christian Fischer
categories: ["musings"]
comments: true
date: 2004-08-19 13:05:24+00:00
layout: post
link: http://blog.invisible.ch/2004/08/19/spot-the-difference/
slug: spot-the-difference
tags: ["blog"]
title: Spot the difference
type: post
wordpress_id: 308
---

Version 1:  

su bea -c "cd /opt/local/somewhere && ./runSomeShellScript.sh"
  

Version 2:  

su - bea -c "cd /opt/local/somewhere && ./runSomeShellScript.sh"
  
  

It took me about an hour to figure out why my installation package (which used version 1) didn't work. Stranger because it worked flawlessly from the commandline. All *nix geeks will already have spotted the difference and LTAO my mistake. 

For all others: the "-" parameter to su specifies that the user should get his own correct environemnt. Without the "-", the new shell process will inherit the environment from the calling process (which -- as it was in my case -- lacked some ENVIRONMENT variables that the script excpected)

I'm one step further in my "unix-do"
