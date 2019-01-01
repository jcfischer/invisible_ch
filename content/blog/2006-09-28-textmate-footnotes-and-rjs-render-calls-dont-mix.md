---
author: Jens-Christian Fischer
categories: ["musings"]
comments: true
date: 2006-09-28 15:10:33+00:00
layout: post
link: http://blog.invisible.ch/2006/09/28/textmate-footnotes-and-rjs-render-calls-dont-mix/
slug: textmate-footnotes-and-rjs-render-calls-dont-mix
tags: ["blog"]
title: Textmate Footnotes and RJS render calls don't mix
type: post
wordpress_id: 559
---

Maybe this saves you a couple of hours of frustration:


    def syslog_progress
      if request.xhr?
        worker = MiddleMan.get_worker(session[:host_info])
        progress_percent = worker.progress
        render :update do |page|
          page.call('progressPercent', 'progressbar', progress_percent)
          if progress_percent >= 100
            page.assign 'stop_polling', true  
          end
        end
      else
        redirect_to :action => 'list'
      end
    end

The RJS calls didn't execute at all and the excessive use of "alert()" to debug neither. Finally, looking at the response in [FireBug][1] I saw that the [TextMate Footnote plugin][2] was adding it's links to the response, rendering the Javascript invalid.

[1]: https://addons.mozilla.org/firefox/1843/
[2]: http://www.agilewebdevelopment.com/plugins/textmate_footnotes


Technorati Tags: [development](http://www.technorati.com/tag/development), [debugging](http://www.technorati.com/tag/debugging), [rails](http://www.technorati.com/tag/rails), [rubyonrails](http://www.technorati.com/tag/rubyonrails)
