---
author: Jens-Christian Fischer
categories: ["musings"]
comments: true
date: 2008-03-14 16:24:11+00:00
layout: post
link: https://invisible.ch/2008/03/14/intldatefield/
slug: intldatefield
tags: ["blog"]
title: IntlDateField
type: post
wordpress_id: 654
---

As promised in the last post, here's my tiny plugin...

and this is the readme:
 
IntlDate
========

Date or DateTime Columns are usually show in forms with the date helpers. However, often you just
want a textfield, instead of the multiple combo boxes. This will work, but dates are displayed 
in the database format (2008-03-13 14:55:44). While that is readable, it's usually not what
your users expect.

To display dates, you can define formats used in the to_s method of the Date objects

    ActiveSupport::CoreExtensions::Date::Conversions::DATE_FORMATS[:ch_dt] = "%d.%m.%Y %H:%M"
    ActiveSupport::CoreExtensions::Date::Conversions::DATE_FORMATS[:ch_d] = "%d.%m.%Y"
    
Wouldn't it be nice, if you could also enter dates in these formats?

Now you can:

* install the plugin

    git submodule add git://github.com/jcfischer/intldatefield.git vendor/plugins/intldatefield
    
* add any DATE_FORMATS to your ''config/environment.rb''
* if you have a textfield for a date column, it will just work


Repository
----------

[https://github.com/jcfischer/intldatefield/tree/master][1]

Copyright (c) 2008 Jens-Christian Fischer, [InVisible GmbH][2], released under the MIT license


[1]: https://github.com/jcfischer/intldatefield/tree/master
[2]: httb://www.invisible.ch


Technorati Tags: [rails](https://www.technorati.com/tag/rails)
