---
author: Jens-Christian Fischer
categories: ["musings"]
comments: true
date: 2005-08-27 05:38:24+00:00
layout: post
link: http://blog.invisible.ch/2005/08/27/lotus-notes-is-not-agile/
slug: lotus-notes-is-not-agile
tags: ["blog"]
title: Lotus Notes is not agile
type: post
wordpress_id: 452
---


[Julian Robichaux](http://www.nsftools.com/) has a recent article "[Agile Development is not for me](http://www.nsftools.com/blog/blog-08-2005.htm#08-24-05)". As you can guess from the title, he's not in the agile camp:


<blockquote>
What's worse is, the "we'll cross that bridge when we get to it" mentality doesn't take into account that there's a certain kind of butterfly effect with software design. A tiny change in architecture at the beginning can have huge impacts later on (for better or worse). Likewise, having to make a seemingly tiny change to core functionality or design later on down the road can be a major undertaking.
</blockquote>


I have been doing agile development for the last couple of years with good results and experiences, both for me and my customers. There is one big caveat though: You will need to work with a technology that supports agile processes.



And Lotus Notes just doesn't.



Sure, all Notes developers can whip up a form and a view in no time at all. We know how to impress clients by building an application in front of their eyes. So we are already halfway at agile development, right? Not so. Notes is a beast when it comes to a couple of extremely important parts of agile development:



There is no support for refactoring.
  
There is no support for automated testing.



And there lies the problem. Agile development embraces change, because there are supporting techniques that make sure, that you won't fall flat on your face when you change that tiny thing down in the foundation of your application. But if you don't have tools for refactoring that change and if you don't have tools that make sure that changes doesn't break a dozen other things in your application you just can't do it.



And that's where other development environments really, really shine. When I code in Java, I use [IntelliJ IDEA](http://www.jetbrains.com/idea/) as an IDE. It's refactoring support is outstanding. It allows me to constantly adapt my code to the way I feel it must be at any given moment. Named something wrong? Change it and be 100% sure that the changes are reflected across all relevant parts of the application. Try that in Notes. Think a field name is wrong? Good luck hunting all the references to it in the tangled mess of forms, views. lookup formulae, Javascript, Lotus Script, hidden forms, computed text and god knows what other goodies the good people at Iris have given us. Yes, there are tools that help: [Teamstudios](http://www.teamstudio.com/) [Configurator](http://www.teamstudio.com/tsv3/teamstudio.nsf/pages/180607DADB22C52585256BF000620156?opendocument&cc=us) is the tool I pay for every year to do Notes development.



Or testing. In Java or in Ruby (more recently) I write extensive unit and functional tests that pound on every aspect of the code I write. Any change I make will either break or pass the tests. When all tests pass, I know that my changes won't break the application. I have tried to implement Unit Test for Lotus Script, and while they have helped on some aspects of development, they just don't cut it. Again, Notes development is the art of managing a dozen different technologies and techniques to make an application behave the way you want it. And unfortunately, there is no way you can test it. So changing a field name is kind of like playing in the lottery: It might work. It might not. You usually find out, when you have deployed the application to the customer and he calls about some error message. Automated testing would have caught that immediately after the change. Unfortunately there is no automated testing.



Those two things make agile development nearly impossible in a Lotus Notes / Domino environment. Using other technologies, they are the way to go.



In my current Ruby on Rails project, we are doing "Agile". Our first delivery to the customer (2 weeks after the project started) showed us two things: Our basic application is working as expected. And our database model is fundamentally wrong. We didn't know in the beginning, because we talked to the domain expert after we shipped the first iteration. We will have to change a lot of the fundamental core of our product. I don't care. I expect this to take not more than a day's work, the larger (and harder) part of which is figuring out the new (hopefully this time) correct data model.



Refactoring & unit tests will make sure, that the rest of the application (UI and functionality) continue to work exactly like they did last week.





Technorati Tags: [agile](http://technorati.com/tag/agile), [arbeitstechnik](http://technorati.com/tag/arbeitstechnik), [domino](http://technorati.com/tag/domino), [lotus notes](http://technorati.com/tag/lotus notes), [development](http://technorati.com/tag/development), [refactoring](http://technorati.com/tag/refactoring), [testing](http://technorati.com/tag/testing), [unittest](http://technorati.com/tag/unittest)
