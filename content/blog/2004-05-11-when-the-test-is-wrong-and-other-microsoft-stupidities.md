---
author: Jens-Christian Fischer
categories: ["musings"]
comments: true
date: 2004-05-11 18:12:48+00:00
layout: post
link: https://invisible.ch/2004/05/11/when-the-test-is-wrong-and-other-microsoft-stupidities/
slug: when-the-test-is-wrong-and-other-microsoft-stupidities
tags: ["blog"]
title: When the test is wrong and other Microsoft stupidities
type: post
wordpress_id: 273
---

_If you provide an option to test something, make sure that it tests the right thing_

The [ZAPPATA crew](https://www.zappatanetworks.com/) was doing some spike testing today with different technologies, and due to the nature of the OS market, we did the tests with the tools most widely in use: Windows XP and Outlook.

The Microsoft-Way is a Wizard-Way. Unfortunately, some of the wizards need wizard like skills to operate or make sense of. One task that is automated by a wizard is the setting up of a new email account in Outlook. The friendly wizard takes you through different questions and sets up the mail account. We were trying to set up an account to a simple POP / SMTP server - but one that requires authentication. So we clicked on the correct options ("My outgoing SMTP Server requires authentication", entered name and password) and then proceeded to click on the big **Test Settings** button provided. It found the POP server, it found the SMTP server, it checked of various other items as successfull and then failed the test of sending a message. Ok - wrong option, or so we thought. We went back to the advanced options. Changed settings. Tested. Fail. Changed settings. Tests. Looked at server logs. 

We determined that Outlook is sending a SMTP HELO command instead of the Extended Hello (EHLO), so it never recognized that the server indeed is looking for an authenticated session. Some googling followed. We found a lot of pages that told us how to set up authentication in outlook [1]. But no mention of our problem. Frustration began to set in. 

Then R. had the idea to just leave the wizard and try to see if at least the retrieval of messages from the server worked. Of course it did. Then for fun, we replied to one of the messages and hit the send button. Lo and behold - Outlook authenticated with the server and delivered the message.

The **Test Settings** button doesn't honor the settings you have made - it just test something entirely different. How very stupid.


1.Did you ever notice how long it takes to describe how to set up something that is done by a wizard? Every step is documented with a screenshot. A simple operation like selecting one checkbox can easily last 3 - 7 pages... Hmm
