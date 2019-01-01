---
author: Jens-Christian Fischer
categories: ["musings"]
comments: true
date: 2003-08-07 11:15:20+00:00
layout: post
link: http://blog.invisible.ch/2003/08/07/when-do-documents-change-their-uniqueid/
slug: when-do-documents-change-their-uniqueid
tags: ["blog"]
title: When do documents change their UniqueID?
type: post
wordpress_id: 154
---

I've been chasing a bug for a couple of hours now.... "Entry not found in index" seems to be a classical @DbLookup that fails... Well, wading through the form, removing blocks of fields, testing again, and again and again and never getting rid of the error on one specific document (but on other everything's fine). The Domino developers know the drill - it's frustrating.

The I looked at the URL - I was opening a doc by it's UNID. I searched for that doc in the database but couldn't find it by that UNID. So I looked at the code that creates the URL. It takes the UNID from a computed field that contains @Text(@DocumentUniqueID).

And guess what - the UNID had changed between when the document was saved the last time and reopened.

The big question: Why does the UNID of a document change, even though it hasn't been updated through the Notes client? (because then the computed field would have the correct UNID)

I suspect [TeamStudios](http://www.teamstudio.com) Configurator (The global search and replace tool for Notes). Anybody know more about that?
