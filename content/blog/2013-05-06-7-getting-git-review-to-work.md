---
author: Jens-Christian Fischer
categories: ["musings"]
comments: true
date: 2013-05-06 11:41:46+00:00
layout: post
link: http://blog.invisible.ch/2013/05/06/7-getting-git-review-to-work/
slug: 7-getting-git-review-to-work
tags: ["blog"]
title: '7 - getting git review to work '
type: post
wordpress_id: 12891
---

Contributing to a large OS project ([OpenStack](https://github.com/openstack)) means to jump through a lot of hoops to get the necessary agreements in place and tools installed.

OpenStack uses [Gerrit](http://en.wikipedia.org/wiki/Gerrit_(software)) for code reviews, and recommends to use git-review for easier review workflow.

The installation is explained in the [documentation](https://wiki.openstack.org/wiki/Documentation/HowTo) and it could be as easy as:

    
    sudo pip install git-review


However that didn't work for me - I was stuck with:

    
    ~ ⮀ git review
    git: 'review' is not a git command. See 'git --help'.


I use [homebrew](http://mxcl.github.io/homebrew/) to install local packages, so the probable cause was some wrong path. It turns out, that pip installs the git-review binary in a non PATH path:

    
    ~ ⮀ sudo pip install git-review
    Downloading/unpacking git-review
     Running setup.py egg_info for package git-review



    
    Requirement already satisfied (use --upgrade to upgrade): argparse in /usr/local/lib/python2.7/site-packages (from git-review)
    Installing collected packages: git-review
     Running setup.py install for git-review



    
    changing mode of /usr/local/share/python/git-review to 755
    Successfully installed git-review


all I had to do then, was to link git-review into my usual binary path:

    
    ln -s /usr/local/share/python/git-review /usr/local/bin


and things started to work. More information on gerrit and the workflows to use it can be found here:



	
  * [http://www.mediawiki.org/wiki/Gerrit/git-review](http://www.mediawiki.org/wiki/Gerrit/git-review)


	
  * [http://www.mediawiki.org/wiki/Gerrit/Tutorial](http://www.mediawiki.org/wiki/Gerrit/Tutorial)


