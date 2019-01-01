---
author: Jens-Christian Fischer
categories: ["musings"]
comments: true
date: 2007-03-22 06:02:06+00:00
layout: post
link: https://invisible.ch/2007/03/22/assert_select-and-url_for/
slug: assert_select-and-url_for
tags: ["blog"]
title: assert_select and url_for
type: post
wordpress_id: 613
---

In the [Extreme Testing][1] presentation, I have a slide with [assert_select][2] examples, some of them lifted from the [assert_select cheat sheet][3]. All fine and dandy, except that this

    assert_select "form[action=?]", url_for( :action => 'foo' )

just doesn't work. `url_for` is a method of the controller, not the ControllerTest class.

So in order to overcome that limitation, you'd need to  

        assert_select "form[action=?]", @controller.url_for( :action => 'foo' )

which doesn't throw an error, but doesn't work either, because `url_for` insists on adding **https://test.host/** to the generated URL. Of course, that's not what's in the form you have generated. What you need to do, is to add the parameter `:only_path  => true` to the `url_for` call:

        assert_select "form[action=?]", @controller.url_for( :action => 'foo', : only_path  => true )

which -- finally -- works, but is very unwieldy.

Luckily, we are working in Ruby, not any other language. Drop this 

    class << self
      def url_for(options, *parameters_for_method_reference)
        options.merge! : only_path => true 
        @controller.url_for(options,  *parameters_for_method_reference)
      end
    end

into the setup method in your functional test, and your set to use:

    assert_select "form[action=?]", url_for( :action => 'foo' )
    assert_select "a[href=?]", url_for( :controller => 'foo', :action => 'bar', :id => @baz) 

as you intended.

[1]: https://www.rails-konferenz.de/2006/redner/jens-christian-fischer/
[2]: https://blog.labnotes.org/2006/07/30/assert_select-rails-core-and-handling-lists-and-tables/
[3]: https://labnotes.org/svn/public/ruby/rails_plugins/assert_select/cheat/assert_select.html





Technorati Tags: [rails](https://www.technorati.com/tag/rails), [ruby](https://www.technorati.com/tag/ruby), [rubyonrails](https://www.technorati.com/tag/rubyonrails), [testing](https://www.technorati.com/tag/testing)
