---
author: Jens-Christian Fischer
categories: ["musings"]
comments: true
date: 2013-02-04 22:54:33+00:00
layout: post
link: http://invisible.ch/2013/02/04/93-error-and-cause/
slug: 93-error-and-cause
tags: ["blog"]
title: 93 - Error and Cause
type: post
wordpress_id: 12135
---

One of the things that make me incredibly happy about my line of work is the following: In every case, when things don't work (there are errors, strange behaviours, weird things) there is a reason. And it is possible to identify the reason, find the cause for the errors and to fix them. I find that very powerful and very reassuring.

There is no such thing as chance or randomness in the errors we encounter. There is a (logical) reason for every glitch, error and problem.

That is the good part. The bad part is that it often is quite difficult to actually track down the root cause and see what the problem is. I have spent my fair share of days tracking down problems... Here are some of the things that I have learnt to help me in finding the problems (in no particular order):


### Write easy to read code


Don't try to be too clever. (And I'm guilty as charged). A cascade of ternary operators might prove that you know your shit (and there even [worse things out there](http://jeremywsherman.com/blog/2013/01/21/the-otherwise-operator/)). Name things properly especially variables and method names. Break methods into smaller ones (see below). Delete unused code (no commenting out stuff). Refactor when you see a possibility for it. Extract objects. Document why you did something (put in that link to Stackoverflow where you found a neat hint in a comment)

None of this is special, or mind boggling new. It is just common sense, and thus, as we usually do with common sense, we ignore it. Don't. You will regret it later...


### Learn to count parentheses and semicolons


The one programming experience that taught me  a lot was to program Lotus Notes formula language. If there is one ugly language (next to [Brainfuck](http://en.wikipedia.org/wiki/Brainfuck)) then it must be the formula language. Check out this little ditty (straight from the IBM documentation)

    
    @If(@Prompt([YESNO]; "Question";
    "Edit this document?");
    @If(@Prompt([OKCANCELEDIT]; "Positive Response";
    "You have chosen to edit this document. Select OK if the name below is correct.";
    @UserName) != "ERR_CANCEL";
    @Command([EditDocument]);@Return(""));
    @Do(@Prompt([OK]; "Negative Response";
    "You have chosen not to edit this document. Select OK to continue to the next document.");
    @Command([NavNext])))


Isn't that a beauty? I have written formulae that spanned several A4 pages. They would either compile - or not. Good luck finding a misplaced semi colon or a missing paren. After a couple of years, I developed an eye for it and could spot syntax errors by just glancing at the code. This skill helps me to this date (although I have grown to dislike languages that have to much noise (Java, PHP, C++))


### Methods longer than 5 lines are suspect


This is a corollary to the things said above: Writing code is hard and difficult. Finding your way through long methods is even more difficult. A method should do one and one thing only. There should only be one way the code is executed (at most two), more complex flow needs to be split up. This will make your methods easier to understand, easier to test and easier to reason about.


### Write unit tests (or specs)


Test all paths through the code, test edge cases, add to your tests when you discover bugs. Run your tests regularly (use a CI server like [Travis CI](https://travis-ci.org/) or [TeamCity](http://www.jetbrains.com/teamcity/) - don't bother with any of the others out there - Jenkins, I'm looking at you). There is nothing better than knowing that your methods are all working correctly and that you can build on stable blocks. If your tests start failing, listen to what they are telling you. Sometimes, they need to be updated to code changes, sometimes they really tell you about bugs that you introduced.


### Write integration tests


If you have complex systems (and chances are that you have complex systems) then you will also need to write integration tests. These need to test as many components of the system as possible (database, services). Currently, I'm the architect of a distributed, service oriented system with around a dozen web services plus a number of other tools involved (databases, message queues). We have integration tests for each of the components, but hardly any tests that tie the whole system together (and we pay a high price for that in terms of making sure new features work - because a new feature usually hits half of the software stack)


### Listen to what your logs and errors tell you


You do have logs? Good - use them extensively. Almost all debug information belongs in the production logs. Matthias Meyer has[ important things to say about log files](http://www.paperplanes.de/2011/7/25/web_operations_101_for_developers.html) (and a lot of other important things too). Your log files can tell you what is happening in your app, but you need to actually read what they say and understand what they are trying to tell you.


### Be methodical


Probably the most important skill to use: You might have a hunch of what went wrong or why. Chances are, that you are wrong. If you have a hunch, find a way to formulate a precise hypothesis and steps how you can test it. Change one thing, test, repeat. When you are satisfied that your hunch was wrong, step back, and formulate another hypothesis. Work your way through your stack, one step at a time. Don't rush, don't cut any corners. This is the part where the men are separated from the boys and where you can either win or loose the fight with your bug.


### The debugger is the absolute last resort


In my younger years I loved debuggers (especially those that allow you to single step through your code). Nowadays I hardly ever use them. They are mostly an enormous waste of time, time that would be better spent writing some more automated tests, or simplifying your code. There's nothing wrong with debugging with print statements (or log entries)


### Know thy computer


Programming in high level languages is all fine and dandy, but you should really know your bits and bytes, you should understand C, pointers, memory allocations, latencies (CPU, Level1 cache, level 2 cache, Ram, Disk, Network), the TCP/IP stack, the Internet protocols you are using, character encodings, and and and. This knowledge will help you time and time again.

(And even knowing this stuff doesn't prevent you from making stupid mistakes.... I recently converted a string that looks something like this "29f44049f34a0b96768f3acca377566df08c3e1c2ff4c700bfdd92d74de68f0c" to a string that contains the decoded hex values. Can you spot the problem?)




## Conclusion


Some bugs are harder to find, some are easier. The methods and tools above will help you along the way. Make use of them, hone your bug killing skills and be glad, that you have a job, that is fundamentally logical.




