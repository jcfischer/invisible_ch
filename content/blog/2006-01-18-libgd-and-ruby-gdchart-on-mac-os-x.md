---
author: Jens-Christian Fischer
categories: ["musings"]
comments: true
date: 2006-01-18 17:32:28+00:00
layout: post
link: http://blog.invisible.ch/2006/01/18/libgd-and-ruby-gdchart-on-mac-os-x/
slug: libgd-and-ruby-gdchart-on-mac-os-x
tags: ["blog"]
title: libgd and ruby-gdchart on Mac OS X
type: post
wordpress_id: 504
---

Trials and tribulations:

## Installing libgd

Use Darwinports to install GD 

    $ sudo port install gd2

(it seems that you need to install gd2, and not gd because otherwise the linker will complain about a function not being defined:

    Arwen:/usr/local/lib/ruby/gems/1.8/gems/ruby-gdchart-1.0.0/examples jcf$ ruby bar_example.rb 
    dyld: NSLinkModule() error
      dyld: Symbol not found: _gdImageCreateFromGif
      Referenced from: /usr/local/lib/ruby/gems/1.8/gems/ruby-gdchart-1.0.0/./GDChart.bundle

it might be a good idea to update your installed darwin ports:

    $ sudo port upgrade installed


## Installing ruby-gdchart

Thanks to the [Pickaxe book and _why][1] for the explanation of the extconf configuration.

Use RubyGems to start the installation of this:

    sudo gem install ruby-gdchart

This will fail because extconf.rb won't find the libgd and complain about it.

Navigate to _/usr/local/lib/ruby/gems/1.8/gems/ruby-gdchart-1.0.0/ext_ and edit *extconf.rb* so that the first couple of lines look like this:

    require 'mkmf'

    dir_config("gd")
    GDCHART_DIR = "./gdchart0.11.5dev"

adding *dir_config("gd")* allows us to specify where the gd libraries are to be found

Then edit ext/gddchart0.11.5dev/Makefile so that the sections *install locations* and *lib gd* look like this:


    # ----- install locations -----
    PREFIX_INC = /opt/local/include
    PREFIX_LIB = /opt/local/lib
    
    # INCLUDEDIRS=-I. -I/opt/local/include/freetype2 -I/usr/include/X11 -I/usr/X11R6/include/X11 -I/opt/local/include 
    
    # ----- lib gd -----
    # GDChart requires the gd library - www.boutell.com/gd/
    # gd 2.0.28 or better is required (GIF support has returned to libgd)
    # if it's not installed in a standard location edit these lines for your installation
    GD_INCL=/opt/local/include/
    GD_LD=/opt/local/lib/
    #GD_LIB=libgd.so
    # a static libgd is also available
     GD_LIB=libgd.a

then run the following command:

    $ ruby extconf.rb --with-gd-dir=/opt/local

This will compile the ruby extension. Now it needs to be installed. Rerun:

    $ sudo gem install ruby-gdchart

to install the newly built library to the correct location. 

This has gotten ruby-gdchart to work on my installation. However, the example files don't seem to work.... Maybe someone else has more info?



[1]: http://www.whytheluckystiff.net/ruby/pickaxe/html/ext_ruby.html#S5



Technorati Tags: [development](http://www.technorati.com/tag/development), [gdlib](http://www.technorati.com/tag/gdlib), [mac](http://www.technorati.com/tag/mac), [rubyonrails](http://www.technorati.com/tag/rubyonrails)
