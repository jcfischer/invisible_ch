---
author: Jens-Christian Fischer
categories: ["musings"]
comments: true
date: 2005-02-28 15:02:56+00:00
layout: post
link: https://invisible.ch/2005/02/28/find-out-which-process-is-listening-on-a-port/
slug: find-out-which-process-is-listening-on-a-port
tags: ["blog"]
title: Find out which process is listening on a port
type: post
wordpress_id: 382
---

If you need to find out which process is listening on a certain port, use the following:

*Linux*
  netstat -natp | grep :80

*Solaris*
  lsof -i | grep :80

On Solaris, you need to have compiled lsof that you can get from [Sunfreeware.com][1]

[1]: https://www.sunfreeware.com
