---
author: Jens-Christian Fischer
categories: ["musings"]
comments: true
date: 2004-09-20 09:29:04+00:00
layout: post
link: https://invisible.ch/2004/09/20/local-web-server-for-windows-with-search/
slug: local-web-server-for-windows-with-search
tags: ["blog"]
title: Local Web Server for Windows with search
type: post
wordpress_id: 322
---

from the **Use-your-readers-as-knowledge-base** dept:

I have a client that has the requirement to have an intranet application available offline and make it available on a CD. Basically it's just a bunch of html files (that originally live in Notes). 

So far, we have exported all the relevant documents using the [Midas Richtext LSX](https://www.geniisoft.com/showcase.nsf/MidasLSX) and stuck them on a CD.

But now, the client wants search too.

I'm looking at the options now. One thing is to use Domino Offline Access. But that would mean major changes to the environment, the application is installed in. (greetings from the IT department). Also it actually does too much -- I just need some browsing and searching.

The second option is to use an off the shelf, mini http server with a search engine. Trouble is, I haven't really found that many options. [Spy CD](https://www.phdcc.com/spy-cd/index.html) is one, but there surely are others out there.

Last option is to roll my own. I have the framework for this with [ZoÃ«](https://zoe.nu) and [Zappata](https://www.zappatanetworks.com). It contains a http server and [Lucene](https://lucene.jakarta.org) for searching. Putting that in place is no more than a couple of hours.

I need:


  * browsing of HTML files
  * Fulltext search of said documents and the PDF, DOC and XLS attachments they contain
  * fully automated CD install (Autorun) and running


All of that as simple as possible and without any trouble to the end-users.

Am I missing a possibility?
