---
author: Jens-Christian Fischer
categories: ["musings"]
comments: true
date: 2003-05-23 22:37:15+00:00
layout: post
link: http://blog.invisible.ch/2003/05/23/domino-5-textfields-to-textareas/
slug: domino-5-textfields-to-textareas
tags: ["blog"]
title: Domino 5 -> Textfields to Textareas
type: post
wordpress_id: 91
---

One of the really cumbersome things in Domino development is the constant struggle to get Domino to do what I want it to do.

Case in point: I have a textfield, but I want to let the user edit the text in a textarea. Domino only displays textareas for RichText fields - which is not at all what I want.

On Notes.net there was a [partial solution](http://www-10.lotus.com/ldd/46dom.nsf/55c38d716d632d9b8525689b005ba1c0/d711e4fa7486fff385256b06004ffc5e?OpenDocument&Highlight=0,textf%3Feld,textarea)... 

Here's the complete one...
<!-- more -->
Create your textfield somewhere (at the top) of the form. Make it hidden.

In your form, create two lines: One for reading, one for editing.

    
    
    <!-- the next line is hidden in edit mode -->
    <div><span>Label:</span><span><computed value></span></div>
    <!-- the next line is hidden in read mode -->
    <div><span>Label:</span><span><textarea name="NotesFieldName" rows="10" cols="50"><computed value></textarea></span></div>
    


Note the computed value? It needs to compute to the field name that you want to edit. (and of course the name of the textarea also needs to be the same as the field you want to edit)

Save the form - and enjoy
