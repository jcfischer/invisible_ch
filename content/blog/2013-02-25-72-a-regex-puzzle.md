---
author: Jens-Christian Fischer
categories: ["musings"]
comments: true
date: 2013-02-25 22:59:50+00:00
layout: post
link: https://invisible.ch/2013/02/25/72-a-regex-puzzle/
slug: 72-a-regex-puzzle
tags: ["blog"]
title: 72 - a regex puzzle
type: post
wordpress_id: 12452
---

Via [Ned Batchelder](https://nedbatchelder.com/blog/201302/a_regular_crossword.html) comes this wonderful Regular Expression Puzzle

[![regular_crossword](/wp-content/uploads/2013/02/regular_crossword.png)](https://www.coinheist.com/rubik/a_regular_crossword/grid.pdf) (Click for PDF version)

Each cell is constrained by three regular expressions, and according to the author of the puzzle, there is one unique solution to it.

We spent around an hour at the office trying to solve it, but only managed around 20 or so cells. That is until JF, our CEO, came in. While he didn't live up to his claim that he'd be able to solve it with his eyes closed, he managed to solve the puzzle at breakneck speed, finishing it at the dinner table. Highly impressive - and good fun!

The comments in Neds post point to a [Haskell solver](https://gist.github.com/LeventErkok/4942496) and a [Python checker](https://gist.github.com/agriffis/4746429). I haven't seen other solvers, but I'd like to try my hands on a Ruby version... Well, one of these days, I guess (which means: never)
