---
author: Jens-Christian Fischer
categories: ["musings"]
comments: false
date: 2006-01-02 20:37:53+00:00
layout: post
link: http://blog.invisible.ch/2006/01/02/where-plugin/
slug: where-plugin
tags: ["blog"]
title: Where Plugin
type: post
wordpress_id: 497
---

UPDATE: I had to disable comments, because I was getting spammed with hundreds of "cool site" messages. Feel free to contact me in any other way.

Working with RubyOnRails is a really wonderful way of developing applications. The [plugin][1] system allows extensions without modifying the core of rails.

Here's my second plugin: _WherePlugin_

It's based on some code by [Ezra Zygmuntovic][2] extended by me, further extended by Ezra and packaged as a plugin.

It allows for easier creation of the :conditions => ... clause in ActiveRecord find statements.

Here's how to use it:

    c = InVisible::Cond.new do
       year '>', 2005
       name 'like', 'Foo%'
    end
    Model.find(:all, :conditions => c.where )

or in a combined form:

    Model.find_with_conditions(:all) do
       year '>', 2005
       name 'like', 'Foo%'
    end

## Installation 

    $cd /my/rails/project
    $ruby script/plugin discover
    $ruby script/plugin install -x where

The subversion repository is located at [http://invisible.ch/svn/projects/plugins/where][3]


## Usage

You can use the following types of clauses in the definition of the Condition block:

  * name 'operator', value
  * name 'between', value, value
  * sql 'some sql statement', value
  
Examples:

  * first_name '=', 'Ezra'
  * start_date 'between', '2006-01-01', '2006-01-30'
  * last_name 'like', 'Zyg%'
  * sql 'hosts.id = something.id'

You can extend an existing condition block like this:

    c = Cond.new
    c < < ['name', 'Jens-Christian']
    c << ['age', '>', 30]

## Caveats

There is one caveat, if you use _self_ in the block:

    Task.find(:all, :conditions => ["project_id = ?", self.id] )

    Task.find_with_conditions(:all) do
        project_id '=', self.id
    end

will break, because _self_ inside the block will refer to another object. A workaround is to use temporary variables:

    self_id = self.id
    Task.find_with_conditions(:all) do
        project_id '=', self_id
    end

I will see, if there is a better solution for this.



## Revision history

v. 0.2 (svn 36), 2.1.2006

  * Added Ezra's Cond Class
  * removed the Where Class (breaking old code, but the Cond class is nicer)
  * fixed the Model.find_with_conditions method to use the Cond class 

  
Comments, ideas etc. very welcome


[1]: http://wiki.rubyonrails.com/rails/pages/Plugins
[2]: http://brainspl.at/
[3]: http://invisible.ch/svn/projects/plugins/where


Technorati Tags: [rubyonrails](http://www.technorati.com/tag/rubyonrails), [sql](http://www.technorati.com/tag/sql)
