---
author: Jens-Christian Fischer
categories: ["musings"]
comments: true
date: 2009-03-04 19:28:31+00:00
layout: post
link: https://invisible.ch/2009/03/04/invisible-rails-sprint-day-3-twurli-comes-alive/
slug: invisible-rails-sprint-day-3-twurli-comes-alive
tags: ["blog"]
title: InVisible Rails Sprint Day 3 - twur.li comes alive
type: post
wordpress_id: 699
---

Today was spent setting up infrastructure. Part of this sprint is to learn new things, so we took the opportunity to play around with some of the new features of Rails 2.3.

The best thing so far is the templating system, that allows you to define which gems, plugins and other files for your rails app. See below for the template we developed. It's based on the [Rails Template Post by Pratik Naik](https://m.onkey.org/2008/12/4/rails-templates).

Another new thing we have tried out: [Clearance](https://github.com/thoughtbot/clearance/tree/master), a authentication system with Cucumber features. We extended it to handle usernames (following [Pikus Blog post](https://ropiku.tumblr.com/post/77138388/clearance-login-with-username).

We didn't get around to implement the Continuous Integration server (we are going to try [Cruise](https://studios.thoughtworks.com/cruise-continuous-integration) by Thoughtworks, instead of the usual [cruisecontrol.rb](https://github.com/thoughtworks/cruisecontrol.rb/tree/master). We'll see how this works out.

So - the teaser page is up, see [twur.li](https://twur.li). By following [twurli](https://twitter.com/twurli) you will be notified when there are news about the site and what it does.

What it does? The name gives a clue...


For the geeks: the template for the Rails app:


