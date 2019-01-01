---
author: Jens-Christian Fischer
categories: ["musings"]
comments: true
date: 2004-03-12 08:41:53+00:00
layout: post
link: https://invisible.ch/2004/03/12/certifiying-an-expired-notes-id/
slug: certifiying-an-expired-notes-id
tags: ["blog"]
title: Certifiying an expired Notes ID
type: post
wordpress_id: 257
---

Dept. My-outsourced-memory

When you move past the expiration date, here's the procedure to recertify a user ID
<!-- more -->
You have a user ID that has expired and you would like to manually recertify it.

The ID can open Notes, because the password is valid, but the user cannot do anything else, as the end date has expired. If the user selects File, Tools, User ID, Certificate, Request Certificate, a message is generated indicating the certificate has expired.

Solution:

The following steps must be performed:

1. Switch to an ID that has Administrator rights.
2. Launch the Notes client.
3. Select File - Tools - Server Administration.
4. For Release 4.x: Click the Certifiers icon. For Release 5.x: Select Administration - Configuration tab, expand Certification and select Certify.
5. Select Certify ID File.
6. From the Choose Certifier ID dialog box, select the O or OU certifier that was originally used to certify the user.
7. Enter the password for the certifier ID.
8. From the Choose ID to Certify dialog box, select the ID to be recertified.
9. Enter the password for the user to be recertified.
10. [Optional] In the Certify ID dialog box, you may set or change the following: Registration server, expiration date of the certifier and password length.
11. Click Certify.
12. Status window displays: "Updating address book entry for username/org", then "Successfully updated address book entry for username/org" and finally "Username/org successfully certified."


[source: [Recertify an expired user ID](https://www-10.lotus.com/ldd/46dom.nsf/55c38d716d632d9b8525689b005ba1c0/f9adecb11dbcb64185256b650051bac8?OpenDocument&Highlight=0,certify,expired,id) ]
