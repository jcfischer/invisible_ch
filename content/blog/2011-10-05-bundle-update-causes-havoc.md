---
author: Jens-Christian Fischer
categories: ["musings"]
comments: true
date: 2011-10-05 08:26:16+00:00
layout: post
link: https://invisible.ch/2011/10/05/bundle-update-causes-havoc/
slug: bundle-update-causes-havoc
tags: ["blog"]
title: Bundle update causes havoc
type: post
wordpress_id: 908
---

You know the feeling - you do a quick "bundle update" and all hell breaks loose? I knew you do.

I updated rspec from 2.5 to 2.6 in one of my projects, and it also updated the nifty [faker](https://faker.rubyforge.org/) gem we use for generating test data.

Of course, this broke a couple of hundred tests with the following message:


    
    <tt>
    NoMethodError:
           private method `rand' called for ["DE", "FR", "IT", "AT"]:Array
    </tt>



I used to select a random country from an array, like thus:


    
    <tt>
    Address.blueprint do
      address_1 { Faker::Address.street_address }
      address_2 { Faker::Address.secondary_address }
      city { Faker::Address.city }
      country { %w{ DE FR IT AT }.rand }
      postal_code { Faker::Address.zip_code }
      state { "new" }
    end
    </tt>



A bit of looking at the faker gems source code, showed me the error of my ways. I shouldn't use the rand method, but either choice or sample instead.

Here's the code that works:


    
    <tt>
    Address.blueprint do
      address_1 { Faker::Address.street_address }
      address_2 { Faker::Address.secondary_address }
      city { Faker::Address.city }
      country { %w{ DE FR IT AT }.sample }
      postal_code { Faker::Address.zip_code }
      state { "new" }
    end
    </tt>




