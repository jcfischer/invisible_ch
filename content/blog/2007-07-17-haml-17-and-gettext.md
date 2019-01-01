---
author: Jens-Christian Fischer
categories: ["musings"]
comments: true
date: 2007-07-17 10:08:12+00:00
layout: post
link: https://invisible.ch/2007/07/17/haml-17-and-gettext/
slug: haml-17-and-gettext
tags: ["blog"]
title: HAML 1.7 and Gettext
type: post
wordpress_id: 626
---

If you are trying to use HAML 1.7 and Ruby Gettext, you'll have problems extracting the string information from the HAML files.

While [teamschnitzel][1] has a solution that almost works, there was a change in HAML 1.7 that will render it useless. HAML deprecated the :precompiled accessor which the GetText Parser needs. Luckily, it's really simple to add it back to HAML:

Open vendor/plugins/haml/lib/haml/haml/engine.rb and

      class Engine
    # Allow reading and writing of the options hash
    attr : options, true
    attr_reader :precompiled

add the attr_reader line. Then scroll down in the file until you see the following code:

    # This method is deprecated and shouldn't be used.
    def precompiled
      $stderr.puts <

Technorati Tags: [gettext](https://www.technorati.com/tag/gettext), [haml](https://www.technorati.com/tag/haml), [rails](https://www.technorati.com/tag/rails)
