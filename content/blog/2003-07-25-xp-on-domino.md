---
author: Jens-Christian Fischer
categories: ["musings"]
comments: true
date: 2003-07-25 18:54:25+00:00
layout: post
link: https://invisible.ch/2003/07/25/xp-on-domino/
slug: xp-on-domino
tags: ["blog"]
title: XP on Domino
type: post
wordpress_id: 137
---

Ben Poole mentions [Testing 1,2,3](https://www.benpoole.com/80256B44004A7C14/perm!open&link=200307251046) in the Notes/Domino context (of course taken from the [Xtreme Programming](https://www.xprogramming.com/) school of thought. He links to [Duffbert's XP experiences](https://hostit1.connectria.com/twduff/home.nsf/plinks/TDUF-5PQGH9).

Let me chime in with my experience on [TestingFirst](https://www.c2.com/cgi/wiki?TestingFirst) with Notes. I worked on a large Domino project last year with a team of 5 other people. I tried to get some XP into the group (but failed - there just wasn't enough interest from the other team members... another story).

From an earlier project I had a NotesUnit Lotusscript class that I expanded and made usable. 
I tried to use it - I tried hard, really hard. Ultimately I just gave up on using it.
Not because I find TestingFirst a wrong thing to do - not at all. It was because the Notes development environment sucks. Our project grew and grew. We built an elaborate LotusScript class library - with about 50-70 classes. Two of us wrote test cases, and tried to execute them every time we changed something. The Notes guys will know that this is not a simple thing to do (You have to run an agent - either locally, or as in our case, on the web server). This turned out to be a slow and complicated process - made worse by the way the LotusScript compiler handles compiling dependecies when base classes change (It doesn't handle dependencies at all - you have to recompile them by hand. We ended up writing our own Classes to generate the dependency tree and compile everything) Then we hit the infamous 64k barrier on size of code - which meant we had to move our code into many smaller libraries (which kills run time behaviour, because the Domino server loads all of the libraries, everytime an agent that uses them is executed) or into fewer, larger libraries that were maintained in external LSS files. We opted for that - but those of you who have been there, know that you're on your own when you have to debug the code. The compiler doesn't help you anymore - it just flags the whole file as being in error - it doesn't even tell you a line number when you make a typo.)
The test-first methodology just didn't help. Testing wasn't anything that was unobtrusive - as it should be in the XP sense, but a major undertaking. But then coding this beast was becoming a major undertaking.
My experiences: NotesUnit works (If there is enough interest from you guys, I'll dig it out and make it available) but the Notes IDE is so bad that it makes grown people cry - specially when you're in large projects.
I haven't had much hands-on time with Notes 6, and I haven't done a project yet with it - but from what I've seen, I doubt that there was much progress in that department - let me know if I'm wrong.
Test first is a great idea, if you code in a language with an IDE that helps you and doesn't throw rocks at you at all times but imo Notes is not ripe yet. 
And that is real shame!
