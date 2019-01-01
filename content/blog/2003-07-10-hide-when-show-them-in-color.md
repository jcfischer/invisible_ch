---
author: Jens-Christian Fischer
categories: ["musings"]
comments: true
date: 2003-07-10 17:18:08+00:00
layout: post
link: http://blog.invisible.ch/2003/07/10/hide-when-show-them-in-color/
slug: hide-when-show-them-in-color
tags: ["blog"]
title: Hide when - show them in color
type: post
wordpress_id: 129
---

I'm doing a lot of quite complex Domino development at the moment. I'm using Hide-When functionality to hide/show pieces of HTML based on various conditions of the document I'm working with. It's a pain to maintain, because it ain't clear what lines are hidden under what conditions. Then it hit me: Why not use color-coding in the form to show what's hidden when:

![color-coded-domino.jpg](http://www.invisible.ch/images/color-coded-domino.jpg)

Red Bold: is hidden when editing (it's bold because otherwise I don't see it as a color blind person)
Green is hidden for reading
Blue is hidden with a formula
Grey for stuff that is always hidden

I'm going to try this and see if it make my life easier. If it does, someone like [Ben](http://www.geniisoft.com/) should make a tool to do this automatically on existing forms
