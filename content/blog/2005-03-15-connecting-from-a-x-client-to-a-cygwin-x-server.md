---
author: Jens-Christian Fischer
categories: ["musings"]
comments: true
date: 2005-03-15 11:31:33+00:00
layout: post
link: https://invisible.ch/2005/03/15/connecting-from-a-x-client-to-a-cygwin-x-server/
slug: connecting-from-a-x-client-to-a-cygwin-x-server
tags: ["blog"]
title: connecting from a X-client to a cygwin X-server
type: post
wordpress_id: 393
---

from the *my-outsourced-brain-dept*:

 * Install [cygwin][1]. Be sure to select the X11 base package
 * open a cygwin shell
 * [start X][2]: `$ startxwin.sh`
 * you will get a xterm window on your Windows box
 * type `$ xhost +` to disable host security, so that other hosts can connect to your server
 * Enable X port forwarding in [PuTTY][3] ( Connections / SSH / Tunnels )
 * connect to the remote machine and start the program that requires X

If all goes well, it will show up on your screen. If you get a "Xlib: connection to ":0.0" refused by server" error message, you have forgot to disable the security by typing xhost +.


[1]: https://www.cygwin.com
[2]: https://x.cygwin.com/docs/ug/using.html
[3]: https://www.chiark.greenend.org.uk/~sgtatham/putty/
