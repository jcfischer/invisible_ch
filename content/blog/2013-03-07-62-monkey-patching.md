---
author: Jens-Christian Fischer
categories: ["musings"]
comments: true
date: 2013-03-07 22:25:02+00:00
layout: post
link: http://blog.invisible.ch/2013/03/07/62-monkey-patching/
slug: 62-monkey-patching
tags: ["blog"]
title: 62 - monkey patching
type: post
wordpress_id: 12625
---

When [I teach my students the beginning points of monkey patching](http://blog.invisible.ch/2013/02/26/71-teaching/) I usually get a gasp or two, a muttered curse and something like "I will never want to maintain something like that". Being the Ruby and Rails developer I am, I console them and tell them that in practice hardly anything bad happens, that Ruby gives you a sharp knife (instead of the plastic implements the Java people get dealt) etc. I also actually believe that this is so.

Today, Alvaro and I were setting up the Mobino stack on a new development machine, and the db:migrate step failed. (It had done so already when I setup Chengchen, but there I was in  a hurry and just installed a DB dump on his machine). Today however, we wanted to find out why it was failing.

We got this weird syntax error:

    
    PG::Error: ERROR: syntax error at or near ")" 
    LINE 1: CREATE UNIQUE INDEX "index_clients_on_email" ON "clients"( ) 
                                                                       ^ 
    : CREATE UNIQUE INDEX "index_clients_on_email" ON "clients"( )


After fiddling around with highly sophisticated debugging techniques for a while (i.e. finding the parts in ActiveRecord that do index creation and littering them with puts statements) we found out that the method didn't receive the columns the index should be built with. Further investigation found that there were not one but three add_index methods in circulation, some of them called another method to get the column names, others called a wrong version of that method... In short - it seemed like a total mess.

Then we realized, that these methods all came from different gems: We use [pg_power](https://github.com/TMXCredit/pg_power) and [postgres_ext](https://github.com/dockyard/postgres_ext) in the project (to support schemas and UUID datatypes). Those two gems were each monkey patching the Postgres ActiveRecord adapter, and of course (of course) those patches were not compatible. This had never been an issue for me before, because those gems only alter the migration statements. They were introduced sometime mid-project, when all tables had been created, so there was never a need to run a full set of migrations again.

We looked at switching the load order around, but that didn't help. Going in and patching the monkey patching didn't seem the most efficient use of our time either. We found a way to run the migrations in two parts (by commenting out each of the two gems in the Gemfile one at a time, bundle installing, running the migrations until they failed, then enabling the gem, bundling and re-running the migrations) which is now documented in the "How to setup a development machine for Mobino" document.

The upcoming Rails 4.0 already has the functionality of the postgres_ext gem built in, so we spent another 30 minutes trying to see if we could easily port the application to Rails 4.0. After having spent 60 minutes on this 30 minutes investigation, we killed the branch we were doing the changes on and made the decision to stay with Rails 3.2 for the foreseeable future...

The moral of this story?

Don't tell your students everything that you have experienced in the wild...
