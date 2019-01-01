---
author: Jens-Christian Fischer
categories: ["musings"]
comments: true
date: 2010-11-15 17:44:01+00:00
layout: post
link: http://invisible.ch/2010/11/15/daily-log-2010-11-15-capybara-callbacks-with-some-phony-thrown-in/
slug: daily-log-2010-11-15-capybara-callbacks-with-some-phony-thrown-in
tags: ["blog"]
title: Daily Log, 2010-11-15, Capybara & Callbacks (with some phony thrown in)
type: post
wordpress_id: 876
---

Preparing for the public demos tomorrow in Lyon...

Florian Hanke is here and has been furiously working on his great [phony](https://github.com/floere/phony) GEM. Phony handles phone number strings and can format them, parse them and do other fun stuff. After this days work, it will be able to tell us, if a phone number is a mobile number, a landline number or a service number. And we need that.

Here's an example of what Phony can do for you:

`
    
    Phony.normalize('1 (703) 451-5115').should == '17034515115'
    Phony.normalize('+41 (044) 364 35 33').should == '41443643533'
    Phony.formatted('41443643532').should == '+41 44 364 35 32'
    Phony.formatted('18705551122').should == '+1 870 555 1122'
    Phony.split('33112345678').should == ['33', '1', '12','34','56','78']
    

`

I found a nasty gotcha in [Capybara](https://github.com/jnicklas/capybara). We use it in our Cucumber features and I had a failing feature in a step that looked like this:
`
    And I fill in "merchant_name" with "merchant gmbh"
`

The field was just empty... Changing the text (merchant gmbh) to something else ("some merchant gmbh" or "blubber gmbh") made Capybare fill out the field. I suspect that there is a problem when the id of the field starts with / is similar to the text being filled in, however I haven't had time to investigate further (and file a proper bug report)

But most of my day was taken up by writing callbacks to different web services. One thing that bit me was that Sinatra doesn't natively parse JSON parameters (we pass them in the request body). Here's the magic incantation we use - there are probably other ways to do it... Feel free to let me know.

`
    
    
      post '/transactions' do
        body = request.body.read.to_s rescue ""
        params = JSON.parse(body)
        transaction = Transaction.create(params)
        if transaction
          status 200
        else
          status 417
        end
      end
    

`
