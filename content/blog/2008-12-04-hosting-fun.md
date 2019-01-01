---
author: Jens-Christian Fischer
categories: ["musings"]
comments: true
date: 2008-12-04 19:43:26+00:00
layout: post
link: http://invisible.ch/2008/12/04/hosting-fun/
slug: hosting-fun
tags: ["blog"]
title: Hosting fun
type: post
wordpress_id: 695
---

We have been moving our clients websites to our own co-located server over the last few weeks and have had mostly good experiences doing so.

Yesterday however, there was trouble in InVisible hosting land, and we had a couple of hours downtime on one of the websites (of course the one with the most traffic...)

So - here's a short post-mortem and the things we did to keep this from happening in the future...

Part1: Installing gems broke a running app - and nobody noticed

We moved a new app to our hosting cluster which is based on Apache2 and [mod_rails](http://www.modrails.com/) and [Ruby Enterprise](http://www.rubyenterpriseedition.com/). This combination has been rock solid for us so far. But the trouble lies in the details... When we installed the RedCloth gem, that the new app needed, somehow the `echoes` gem got trashed/removed/whatever. This caused another application to fail and displaying the (really helpful) error message that mod_rails provides. (No sarcasm there: the error messages by mod_rails tell you exactly what is wrong; good stuff). We first noticed this, when we received an email from the client... Bad! 

Monitoring! I can hear you say, You should use monitoring.... But we do! We use [Scout](http://scoutapp.com) to monitor all our websites. So why didn't we get notified? Because the website - to Scout - still seemed up! The error message was a regular web page, HTTP Status code 200 - everything fine, at least for Scout.

This led to some scout-plugin programming, and we came up with a slightly modified url monitoring plugin that additionally looks for some text on the returned page. That should solve that problem for good...

The code for this plugin is on our github repository: [jcfischer/scout-plugins](http://github.com/jcfischer/scout-plugins/tree/master) 

As if that wasn't enough, in the afternoon, mod_rails (or rather one of the rails apps served) started spinning in a thight loop and got stuck. Eventually we had several spawned rails apps, each with 50 requests queued up, the CPU at full load and all other rails apps ground to a halt.

I'm not sure why this started to happen: the offending rails app had been running for weeks without problems. I installed mod_rails 2.0.4, enabled the [global queue feature](http://blog.phusion.nl/2008/10/29/phusion-passenger-now-with-global-queuing/) and have been watching the server all day. So far everything seems fine, but we'll have to track that for longer...

At the same time, I fixed the rails_request plugin for scout to handle the new production.log format of Rails 2.2 applications. It too is in our scout-plugins repository.

Let's see, how well behaved our Rails Hosting environment is in the next few days.
