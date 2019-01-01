---
author: Jens-Christian Fischer
categories: ["musings"]
comments: true
date: 2011-10-13 15:17:07+00:00
layout: post
link: http://blog.invisible.ch/2011/10/13/getting-a-java-jax-ws-service-created-with-intellij-10-5/
slug: getting-a-java-jax-ws-service-created-with-intellij-10-5
tags: ["blog"]
title: Getting a Java JAX-WS service created with IntelliJ 10.5
type: post
wordpress_id: 1042
---

  
(These are just notes for myself, if you know anything about this, then feel free to correct, improve)  
  
* Use the new project wizard to create a web service (with JAXWS selected)  
* optionally, select the Tomcat Webserver (so that you can deploy from IntelliJ to Tomcat directly)  
  
IntelliJ creates a HelloWorld class and everything works fine when you use it. However, if you create your own class, Tomcat complains about some proxy classes not being available (failed to parse runtime descriptor: runtime modeler error: Wrapper class bla.fasel.jaxws.CreatePdf is not found. Have you run APT to generate them?  
com.sun.xml.ws.model.RuntimeModelerException: runtime modeler error: Wrapper class bla.fasel.jaxws.CreatePdf is not found. Have you run APT to generate them?)  
The magic incantation to get this working:  
  
* In your class file, right click and select "Web Services -> Expose Class as Web Service" - in theory, that should create the proxy classes, but doesn't  
* Again in the class file, click "Web Services -> Create WSDL from Java File"  
  
IntelliJ creates a bunch of wsdl and xslt files  
  
Drop to a console and run the following command:  
  
xjc bla/fasel/FopServicePortType_schema1.xsd  (change filenames accordingly)  
  
This creates 4 java files (or more, depending on how many methods you expose)  
  
Create new directory "bla/fasel/jaxws" and move those new Java files into the directory.  
  
Open each file and fix the package statement (was: "bla.fasel", needs to be: "bla.fasel.jaxws")  
  
Compile, deploy - wonder why you are doing this in Java instead of better environment (like Ruby) and then remember that the support for Ruby SOAP Servers is as bad as this...

**Google+:** [View post on Google+](https://plus.google.com/109789939743085010576/posts/CEZsuobUb6j)

  
  
_Post imported by Google+Blog.  Created By [Daniel Treadwell](http://minimali.se/)._
