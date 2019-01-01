---
author: Jens-Christian Fischer
categories: ["musings"]
comments: true
date: 2006-11-12 18:18:17+00:00
layout: post
link: http://invisible.ch/2006/11/12/did-i-mention-that-i-love-ruby/
slug: did-i-mention-that-i-love-ruby
tags: ["blog"]
title: Did I mention that I love Ruby?
type: post
wordpress_id: 566
---

I'm busy coding an application, and I needed to find out if some value is included in one of several arrays:

    a = [ 1, 2, 3 ]
    b = [ 2, 3, 4, 5 ]
    x = 5
    y = 6

Now the question is: Is x in either Array a or b?

    arrays = [a, b]
    arrays.inject(false) { |is_in, array| is_in or array.include?( x ) } # => true
    arrays.inject(false) { |is_in, array| is_in or array.include?( y ) } # => false


Beautiful! (or is there a better way?)


Technorati Tags: [ruby](http://www.technorati.com/tag/ruby)
