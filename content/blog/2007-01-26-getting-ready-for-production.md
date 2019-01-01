---
author: Jens-Christian Fischer
categories: ["musings"]
comments: true
date: 2007-01-26 17:17:50+00:00
layout: post
link: http://invisible.ch/2007/01/26/getting-ready-for-production/
slug: getting-ready-for-production
tags: ["blog"]
title: Getting ready for production
type: post
wordpress_id: 588
---

The [secret project][1] I'm working on is taking shape. And because of the looming deadline ([Liftconference][3] coming up fast), I had to give some thoughts on the hardware, I'm deploying this application on...

I have been a [Textdrive][2] (affiliate link) customer since ever they existed. I have seen them grow from a small hosting company with only a couple of servers to being bought by [Joyent][4] (of which there will be talked more soon). Joyent/Textdrive has spent the last couple of months moving their complete hosting infrastructure from Dell Servers running FreeBSD to Sun Servers running OpenSolaris. They have told numerous tales about how much their hosting experience has improved. 

They have been offering something they call "Containers", pieces of a SunFire 4100 server with 4 Dual Opterons, 16 GB of RAM. So for this project, I decided to use their 1/16 container. This basically guarantees me that I always have 1/16 of the resources of this machine available. If no one else is using CPU, I can have it all... Wonderful :-)

Setting up the container with a Apache / Mongrel / Rails / PostgreSQL stack took about 3 hours, most of the time researching the differences between Linux and Solaris command line parameters and getting used to the different layout. There are [lot of helpful posts][5] on the Textdrive forum, that got me going. 

The the big disappointment. My app took multiple seconds to load - not quite what I was expecting from this machine. Network latency was (and continues to be) one problem: I see roundtrip times of about 200ms to this machine. But the real culprit was the Apache / Mongel combo on serving static files. I had heard good things about [nginx][6], a russian made server/loadbalancer and decided to use it. I got it up and running quite easily:

    ./configure --with-http_ssl_module --sbin-path=/opt/csw/bin --prefix=/opt/csw/nginx
    make 
    make install

which drops it into the /opt/csw tree. I then used Ezra's [config file for nginx][7]. Finally, I modified an existing SMF file to get nginx to (re)start on reboots and being monitored by the Solaris Management System SMF. Here's my nginx.smf file:

    
    
    
      
        
        
        
          
        
        
          
          
        
        
          
        
        
          
            
            
              
            
          
        
        
          
        
      
    

it can then be imported and enabled with the following commands:

    # svccfg import nginx.smf
    # svcadm refresh network/nginx
    # svcadm clear network/nginx
    # svcadm enable network/nginx

And boy did that make a difference. The load time dropped down a lot, and serving of static files is much, much faster (and with caching enabled) almost instantaneous.

Now we'll have to see, how the container holds up, when the masses are unleashed upon the application I'm writing...


[1]: /2007/01/12/this-is-one-crazy-month/
[2]: http://www.shareasale.com/r.cfm?B=69506&U=196165&M=10198
[3]: http://liftconference.com
[4]: http://www.shareasale.com/r.cfm?B=57232&U=196165&M=10198
[5]: http://forum.textdrive.com/viewforum.php?id=37
[6]: http://nginx.net/
[7]: http://www.brainspl.at/articles/2006/09/12/new-nginx-conf-with-rails-caching



Technorati Tags: [joyent](http://www.technorati.com/tag/joyent), [nginx](http://www.technorati.com/tag/nginx), [textdrive](http://www.technorati.com/tag/textdrive), [rails](http://www.technorati.com/tag/rails), [smf](http://www.technorati.com/tag/smf), [solaris](http://www.technorati.com/tag/solaris)
