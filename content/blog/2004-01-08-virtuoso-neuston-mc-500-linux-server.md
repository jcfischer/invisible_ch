---
author: Jens-Christian Fischer
categories: ["musings"]
comments: true
date: 2004-01-08 21:02:54+00:00
layout: post
link: http://invisible.ch/2004/01/08/virtuoso-neuston-mc-500-linux-server/
slug: virtuoso-neuston-mc-500-linux-server
tags: ["blog"]
title: Virtuoso Neuston MC-500 & Linux Server
type: post
wordpress_id: 232
---

I [recently](http://www.invisible.ch/archives/000214.html) got a [Neuston Virutoso MC-500](http://www.neuston.com/en/mc500.asp) streaming media client. A nice box that really does what it's supposed to to: Stream music and videos to my TV and living room amplifier.

The only drawback: It requires a windows PC as a server. I have moved all my media to a little fanless Debian box and was hoping to stream my media from there.

Enter the [OpenShowCenter](http://openshowcenter.sourceforge.net) which is for Pinnacle streaming systems but works equally well for the MC-500.

Here's how I had to install it:


  * copy the OSC files to my `/var/www` directory (that's the Apache root directory
  * add the following to my `httpd.conf`:

`# The Neuston expects it's server on port 8000  
Listen 8000  
[...]  
LoadModule php4_module /usr/lib/apache/1.3/libphp4.so  
[...]  
<Directory />  
  DirectoryIndex index.php  
  Options SymLinksIfOwnerMatch  
  AllowOverride None     
</Directory>  
`
  * Restart Apache
  * create a new server entry on the Neuston, entering the IP Address of the server like this: 192.169.1.100:8000
  * Connect to the server and enjoy

When I had that, everything worked, except the actual streaming of the media on the server. Turns out, I had `Port 80` in my httpd.conf and the PHP module took that when creating the entries for the playlist. I fixed it by changing the portnumber in the `playlistgen.php` scripts (but only because I found the Port 80 statement too late...

Happyiness and a streaming Linux server
