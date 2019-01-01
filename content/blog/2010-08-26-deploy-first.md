---
author: Jens-Christian Fischer
categories: ["musings"]
comments: true
date: 2010-08-26 19:58:45+00:00
layout: post
link: http://blog.invisible.ch/2010/08/26/deploy-first/
slug: deploy-first
tags: ["blog"]
title: Deploy first!
type: post
wordpress_id: 841
---

I'm in the middle of starting a (potentially) huge project with a couple of friends. Having just finished (well, technically, almost finished) a large enterprise Rails project, I am really looking forward to working in a small agile team, on an extremely tight deadline, but doing stuff that is relevant and interesting. 

The enterprise project was an interesting experience, partly because of the technology stack we had to use: Rails on JRuby, developing on Windows machines (which is so painful, you just want to give up) and deploying on Websphere (bad) on zLinux (think IBM big iron) with a host DB/2 database. Lot's of challenges right there, and lot's of learning.

One of the things, our Scrum coach [Michael Mahlberg](http://agile-aspects.blogspot.com/) (and good friend after a year of working together) taught is the importance of continuous integration (no, not having CI servers, but living a strict process) and the need for an early deployment. In the project we were able to deploy to the foreign stack early on in the project, something that helped us a lot, because we were able to convince the IT architects, that there are good things to the madness we were propagating (Ruby, RubyMine, Git, BDD, Scrum - each one new and unknown). 

A few months ago, Michael shared a link to a Kent Beck article, [Continuous Deployment Immersion](http://www.threeriversinstitute.org/blog/?p=488) that suggested the crazy idea that the first thing a team should to, is to fully automate the deployment process before developing any code. This jives nicely with my view of the (software) world, and at one I had our CI server set up to deploy an application on every successful commit. 

The very first thing we did in the new project was to write a small prototype / proof of concept that would illustrate the basic idea. We got this up in 5 days and got it deployed on [our own servers](http://invisible.ch/dienstleistungen/hosting/). Now that we are developing for real, it was time to redo the deployment. We are going to be using Amazon EC2 for our site, with a variety of servers talking to each other. Right now, our zoo consists of PostgreSQL 9 (in beta right now), Rails, a couple of Sinatra and Ruby apps, Redis and [Freeswitch](http://freeswitch.org), a VOIP server, similar to Asterisk. I wanted to have a stable way of deploying both the technology stack and the applications before actually developing the applications, in order to being able to demonstrate our growing product to potential customers right from the start. 

At this years RailsWayCon, I saw a demo of [Scalarium](http://scalarium.com), a service on top of EC2 that allows for deploying and auto-scaling and healing of complex web applications. Scalarium is built by the friendly folks at [Peritor](http://www.peritor.com/) whom I have met several times at conferences. They have built an impressive infrastructure, using [Chef](http://www.opscode.com/chef/) as the tool to automate their builds. In order to kickstart our process and transfer some knowledge, I invited [Matthias Meyer](http://www.paperplanes.de/) to Zurich, and we spent a day working on the deployment.

The end result? We can bring up our cloud fully automated, all applications running in a matter of minutes. Extending capacity (should it become necessary) is a mouse click away. 

Now we can begin development in earnest, knowing that we can deploy our complex application at moments notice. 
