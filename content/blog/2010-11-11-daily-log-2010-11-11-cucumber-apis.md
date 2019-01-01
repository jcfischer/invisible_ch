---
author: Jens-Christian Fischer
categories: ["musings"]
comments: true
date: 2010-11-11 18:02:30+00:00
layout: post
link: http://invisible.ch/2010/11/11/daily-log-2010-11-11-cucumber-apis/
slug: daily-log-2010-11-11-cucumber-apis
tags: ["blog"]
title: Daily-Log, 2010-11-11 - Cucumber & APIs
type: post
wordpress_id: 872
---

We are using a lot of distributed Sinatra and Rails3 applications in our [Mobino](http://mobino.com) project. They speak HTTP-REST and JSON with each other. Because we are using Cucumber and RSpec, we also have some high level integration tests for the APIs. 

Today I started on cleaning up an API in the Rails app. I wrote a cucumber step to invoke the API. It took me a while to figure out the magic incantation to make the controller retrieve the parameters as JSON: Here's the relevant part of the step_definition:

`
    
    
    When /^an API transaction from (client \w+) to (merchant \w+) over (amount \d+\.\d+) is made$/ do |client, merchant, amount|
      path = '/api/transactions'
      params = {:debitor_id => client.id, :creditor_id => merchant.id,
                :amount     => amount}.to_json
      post path, params, {"CONTENT_TYPE" => "application/json", "ACCEPT" => "application/json" }
      response.status.should == 201
    end
    

`

The key to success was to pass the hash with the content type and the accept headers - but specifying them like Rack variables, not HTTP Headers.

Another nice thing I discovered today was the **Transform** in Cucumber. It allows you to DRY up your steps by moving code that works on the arguments you provide (for example code that loads some object from the database) into it's own transform step. 

`
    
    
    Transform /^merchant (\w+)$/ do |name|
      Merchant.find_by_login name
    end
    
    Transform /^amount (\d+\.\d+)$/ do |amount|
      amount.to_f
    end
    

`

More details on this technique over on the [Cucumber Wiki:Step Argument Transforms](https://github.com/aslakhellesoy/cucumber/wiki/Step-Argument-Transforms) and an [Engine Yard blog post](http://www.engineyard.com/blog/2009/cucumber-step-argument-transforms/).

