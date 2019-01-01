---
author: Jens-Christian Fischer
categories: ["musings"]
comments: true
date: 2003-07-25 07:40:21+00:00
layout: post
link: http://blog.invisible.ch/2003/07/25/the-browser-the-one-user-interface/
slug: the-browser-the-one-user-interface
tags: ["blog"]
title: The browser - the one user interface?
type: post
wordpress_id: 132
---

Tim Bray makes a case for not being a "sharecropper" and [developing for the browser only](http://www.tbray.org/ongoing/When/200x/2003/07/12/WebsThePlace) or rather - to code to open standards, XML, RPC etc. and so on. 
I agree 100% - that's a good thing to do. But he makes the case, that the browser is the best thing that happened to interface design and application design since sliced bread:


<blockquote>But it's especially good for the customers to be on the Web platform. The notion of routing everything through the browser (with one significant exception, which I'll discuss below) is incredibly user-centric, user-friendly, and user-empowering. Because once they know how to use the "Back" button, to click on highlighted text, and to fill out a form, then they don't need much training in how to use your application.</blockquote>


and


<blockquote>Which is not to say that the browser is the right answer for everything. Here's an overgeneralization which I think works. Computer applications, excluding games, fall into one of three baskets: information retrieval, database interaction, and content creation. History shows that the Web browser, or something like it, is the right way to do the first two. </blockquote>


I disagree! The browser, while good for - well - browsing, makes a lousy tool for interaction with rich data. And no, I'm not talking about Flash presentations. Browsers are slow. If it's not the missing bandwidth that's killing your application, then it's the slow application server you're running on. Or the different version of IE that are deployed in the corporation. If all of that's ok, then it's your users, that don't understand that for certain things (like interacting with a database), modality is necessary thing and the back button is evil.
Things can go wrong in all the wrong places when you have an app that is totally browser centric. Did I mention that it's slow?
You might argue that all of these bad things wouldn't happen, if I coded better. That might be... But: Is it really the developers duty to build an application that consists mainly of quirks to simulate a better application environment? Take modality: There are times, when modality is needed. In order to absolutely, positively make it impossible for the user of a browser based application not to close a window, or close the underlying window or not hitting the back button, or not taking the focus away of the modal dialog or... I have to jump through a dozen hoops,  juggling and singing the "the browser is a great interface abstraction"-mantra at the same time. Hmm - I'd rather spend my time on the businesslogic than on this.

I am biased: I have worked with the Notes / Domino client for over a decade (13 1/2 years now) and I have grown to like the interaction capabilities a well designed application. (And I know - there are horrible Notes applications as well - don't get me wrong. I know them and I'm guilty of developing some of them)


<blockquote>That's why the phrase quoted above, about flexibility and usability, is so completely 100% wrong. Browsers are more usable because they're less flexible.</blockquote>


Then let's get back to 3270 terminals - if you like even less flexibility. And - quick: Tell me the difference between a web browser and a 3270 terminal. Fundamental differences only, please.
Lack of graphics. Other than that: Full web browser feature set: 

  * Display text
  * follow a rigid menu structure (links)
  * fill out forms

So what is the right way to do things?
I don't think there's a clear black/white answer. The browser is great for a lot of things - and for information retrieval it's great. But as soon as interaction is involved - more than casual interaction that is - the browser starts to suck. 
If you don't want it to suck, then you have to develop applications in HTML - which certainly is possible, but leads to the problems mentioned above.
I'm not arguing that everybody should use VB or the .NET-du-jour tool or do everything in Java. But there are areas of interaction with data in the browsing - database interaction - content creation continuum that benefit from a FAT client (like Notes).
There are of course exceptional browser based application: I discovered [Oddpost](http://www.oddpost.com/) a while ago, last I week I stumbled on [Convea](http://www.convea.com/) - beautiful applications that are so far away from being "browser" that it's scary. But then - look at the effort it takes to get to that stage. Hmm - or maybe that's the point? Maybe it is easier to code a web based application like Convea in DHTML and ASP and Javascript then to write an Outlook clone in C++? 

Let me take some time to think about that....
