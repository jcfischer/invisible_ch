---
author: Jens-Christian Fischer
categories: ["musings"]
comments: true
date: 2009-04-29 21:38:38+00:00
layout: post
link: http://invisible.ch/2009/04/29/amazon-s3-heroku-and-the-paperclipped-assets-manager-for-radiant/
slug: amazon-s3-heroku-and-the-paperclipped-assets-manager-for-radiant
tags: ["blog"]
title: Amazon S3, Heroku and the Paperclipped Assets Manager for Radiant
type: post
wordpress_id: 703
---

Well this is my first post since joining Jens-Christian and Daniela here at InVisible, but the topic is an old one. About a year ago I released the [Paperclipped Assets manager](http://github.com/kbingman/paperclipped/tree/master) for Radiant, which started rather slowly, but has recently taken off and become quite popular. Thanks to the magic of [github](http://github.com), I have received numerous patches and improvements and it has begun to take shape. 

With last week's announcement of pricing by [Heroku](http://heroku.com) and their recent blog about installing Radiant, I decided to give it a try. And, much to my surprise it works really well. Getting used to the read-only file system is certainly something new, but it is surprisely easy and very fast. I love being able to push and pull the database at will, which for small sites in Radiant is a real must to keep everything in sync. 

But of course, Paperclipped no longer worked. It uses the file system by default, which just doesn't work in a read only world. But [Paperclip](http://github.com/thoughtbot/paperclip/tree/master), the wonderful plugin by [Thoughtbot](http://thoughtbot.com/) that powers it all supports S3 out of the box. I had used it before with no problems and modfying the extension proved to be very easy. 

Everything works as before, but now if you want to add S3 support, you simply set the storage setting to "s3". 


    
    <code>Radiant::Config[assets.storage] = "s3"</code>


 
Then add 3 new settings with your Amazon credentials, either in the console or with the [Settings](http://github.com/Squeegy/radiant-settings/tree/master) extension:


    
    <code>Radiant::Config[assets.s3.bucket] = "my_supercool_bucket"
    Radiant::Config[assets.s3.key] = "123456"
    Radiant::Config[assets.s3.secret] = "123456789ABCDEF"
    </code>



and finally the path you want to use within your bucket, which uses the same notation as the Paperclip plugin.


    
    <code>Radiant::Config[assets.path] = :class/:id/:basename_:style.:extension 
    </code>



The path setting, along with a new `url` setting can be used with the file system to customize both the path and url of your assets as well. No more forking for something as silly as a new path. 

Once this is all set, be sure that you have the right_aws gem installed and restart the server and you should be using s3. 

The next step is to get some dynamic thumbnail generation going, so that you can do something like


    
    <code>  <r:assets:image size="new_thumbnail_size" geometry="100x100#" /></code>


  
and then paperclip will make a new square thumbnail unless one exists.

But that is not quite ready for prime time...

Again thanks for all the patches and please keep them coming. 

And for those of you going to the RailsConf next week, I will be hosting a [Birds of a Feather](http://en.oreilly.com/rails2009/public/schedule/detail/9204) session on Tuesday at 8:30pm. Hope to see you there!

Keith

