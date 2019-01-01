---
author: Jens-Christian Fischer
categories: ["musings"]
comments: true
date: 2003-09-03 07:26:31+00:00
layout: post
link: http://blog.invisible.ch/2003/09/03/fixing-links/
slug: fixing-links
tags: ["blog"]
title: Fixing links
type: post
wordpress_id: 172
---

As mentioned yesterday, I had to do a bit of work on an application that included the possibilty of redoing some 15000 links.

Here's what's happened:
I'm maintaing a Notes application for a corporate manual. This manual get's revised every 6 months, with new versions being put out. The revision coming up is major, so we decided to fork the manual (i.e. creating a new copy of it to work on) instead of using the built in workflow process to handle the changes with draft documents.

Unfortunately, the documents are heavily hyperlinked with Notes doc Links. And the workflow process also uses doc links. Now Doclinks point to internal document identifiers that you, as a user, has no control over. Luckily, when copying a complete database, doclinks maintain their "linkage" even though they now physically are in a complete new database. (When you only copy one document from one database to another, the links aren't updated and any link in the copied document still points to the "old" database)

What I was left with, was a database that had a lot of working links, some links that didn't work and an unknown number of links that might or might not work.

To add to the confusion, the users had been busy creating links between new documents that were in draft mode. A bad thing to do in this particular application, because the workflow process would later copy the contents of the new document over the old document (precisely to avoid the problem of broken links). However, in the case of new documents, there was no old version of the document, but there was still a new document created with a different internal ID.

Basically we were running headlong into a mess... The deadline for fixing all of this? A mere two weeks.

So what did I do? As a first measure, I wanted to know how bad the situation really was: I spent a lot of money on [Linkchecker from TeamStudio](http://www.teamstudio.com/tsv3/teamstudio.nsf/pages/32B5601CEADD607685256C210045CEDB?opendocument&cc=us). (I like the TeamStudio tools and have been using them for years. My all time favorite is [Configurator](http://www.teamstudio.com/tsv3/teamstudio.nsf/pages/180607DADB22C52585256BF000620156?opendocument&cc=us) which allows me to do search/replace across a whole database - but I use it to find all occurences of a string mostly)
Anyway: Linkchecker showed me 15'000+ broken links... Ups!
Not good. Not at all good.
In order to get these kinds of problems out of the way, I decided to implement a new linking scheme. Because we were going to not use the Notes client for readers in the future anyway, I could do a URL based link scheme. Every document got a new UniqueID (@Unique) and can now be referenced by that.
Then I got a copy of [Ben Langhinrichs](http://www.geniisoft.com/showcase.nsf/GeniiBlog) [Midas LSX for Richtext](http://www.geniisoft.com/showcase.nsf/MidasLSX) that allows almost any kind of manipulation of RichText and all the kind of embedded things in it.
Ben helped me with very fast email support and a couple of hours later I had a short agent that found the doclinks and converted them to URL links, doing text formatting (blue underlined) on the way.
The result?
I'm left with 72 broken links - that are really broken. And LinkChecker points me to them. 
It's as I [always say](http://www.invisible.ch/archives/000032.html): Get the right tools for the job!
