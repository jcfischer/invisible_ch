---
author: Jens-Christian Fischer
categories: ["musings"]
comments: true
date: 2005-03-10 22:32:39+00:00
layout: post
link: http://blog.invisible.ch/2005/03/10/automated-testing-of-domino-web-applications/
slug: automated-testing-of-domino-web-applications
tags: ["blog"]
title: Automated Testing of (Domino) Web Applications
type: post
wordpress_id: 388
---

Developing web applications is one thing, testing them another. Sure there are Unit tests, functional tests but in the end, the application also needs to be tested as the clients and users see it. And too many times, a seemingly simple change in an application breaks down parts of the application that weren't regression tested.

Unfortunately, testing an application in a browser is difficult at best, sometimes impossible. As soon as JavaScript functionality enters the picture, there doesn't seem a way around long clicking exercises. The testing frameworks that have been available so far, aren't really suited to the task. Enter [Selenium][1] by a couple of Thoughtworks engineers. 

Selenium tests the application inside a web browser. IE, Mozilla and Opera - with some funky problems - are supported. It consists of a couple of Javascript functions that drive the application that sits inside an iframe in the testing browser. Tests are written by creating html files with tables. Each row in the table defines one command ( open this url, follow this link, click on that button, enter that text, check for a text or value, etc). These commands allow you to script most of the interactions with a web application. These scripts can then be run after changes have been made to the AUT (Application Under Test), catching all those "just a tiny change that won't really matter" changes, that most of us have been guilty of doing.

I have put together a Notes Database, [NotesSelenium][2] that contains the mail Selenium features. Copy a couple of design elements into your own Domino application, write a couple of test documents and you are set to test you applications.

There are a couple of example test in the database to give you a (very basic) idea on how to set up your tests. These tests are actually testing parts of NotesSelenium itself. And - believe it or not - while fiddling around the database (doing some layout and hide-when) stuff, the tests actually caught that I had hidden an input field on the web. Lesson: There is no such thing as a minor change, that surely will not affect anything. And using the right tools, you will find those buggers faster.

Enjoy & Feedback welcome

Selenium will go into all of my Notes applications and using it should increase the quality of those applications. I personally have been bitten too many times to not know, how important testing is. And I'm glad that finally there seems to be a solution that does these kinds of tests.

**Update:** Fixed the link to the download

[1]: http://selenium.thoughtworks.com
[2]: http://blog.invisible.ch/files/NotesSelenium-0.1.zip
