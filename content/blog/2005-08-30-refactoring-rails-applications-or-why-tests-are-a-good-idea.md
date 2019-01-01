---
author: Jens-Christian Fischer
categories: ["musings"]
comments: true
date: 2005-08-30 13:43:48+00:00
layout: post
link: http://blog.invisible.ch/2005/08/30/refactoring-rails-applications-or-why-tests-are-a-good-idea/
slug: refactoring-rails-applications-or-why-tests-are-a-good-idea
tags: ["blog"]
title: Refactoring Rails Applications or why tests are a good idea
type: post
wordpress_id: 454
---


Somewhat of an add-on to the post "[Lotus Notes is not agile](http://blog.invisible.ch/archives/000452.html)". 



The project I'm working on with the good folks of [sourcepole](http://sourcepole.ch/), is a network monitoring tool. We are using [Ruby on Rails](http://rubyonrails.org/) to build a web frontend to some Ruby Network monitoring-fu. The network topology is stored in a database, and in our first delivery we got the fundamental database design wrong. So I spent half a day thinking about a new database model and spent the remainder of the day to build a quick spike to test if the new database model would be able to sustain the requirements. This remaining day was spent over the weekend with much cursing and muttering, but finally it seemed to work.



Yesterday afternoon I implemented the new database tables, renamed a couple of models, introduced some new ones. Because a fundamental change like this is likely to break all kinds of stuff, I used our suite of unit and functional tests to figure out, where the application breaks. After 3 hours of changing code and adapting tests, I got the unit tests running:

    
    
    Started
    ....................................
    Finished in 70.068743 seconds.
    36 tests, 127 assertions, 0 failures, 0 errors
    


Then, with only very small changes, I had the main UI functional test up and running. The I ran into a major problem: One of the functional tests complained that:TypeError: Node is not a class



This was in the code that imports an XML representation of the database contents. In refactoring, I had changed one of my classes to be a **Node**. Bad idea if you are using REXML. So I had to go through all the code again to change Node to something more specific. Again the tests helped me identify all areas in my code, where Node was referenced. 



In the end I had both unit and functional test running again. I fired up the application itself (which I hadn't started since beginning this remodelling project) and - hey presto: It worked right away, using the new database model, and improved in it's functionality.



The power of unit & functional tests made this major piece of surgery possible with very little effort. Ruby and Rails both helped, in making the whole experience enjoyable. And to come back to the post about Notes: I don't think that would have been possible in Notes - even though I have some 14 years of experience in developing for it.





Technorati Tags: [agile](http://technorati.com/tag/agile), [automatisch](http://technorati.com/tag/automatisch), [development](http://technorati.com/tag/development), [domino](http://technorati.com/tag/domino), [lotus notes](http://technorati.com/tag/lotus notes), [rails](http://technorati.com/tag/rails), [refactoring](http://technorati.com/tag/refactoring), [testing](http://technorati.com/tag/testing), [unittest](http://technorati.com/tag/unittest)
