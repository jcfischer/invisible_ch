---
title: "Responsive Images"
date: 2019-01-19T22:09:27+01:00
author: "Jens-Christian Fischer"
description: "Adding a shortcut to generate responsive images"
image: ""
categories: ["code"]
tags: ["hugo", "responsive", "images", "html"]
language: en
slug:
type: post
---

My quest for a [slimmer website](/2019/01/slimming/) is ongoing. The newest addition tackles 
[responsive images](https://developer.mozilla.org/en-US/docs/Learn/HTML/Multimedia_and_embedding/Responsive_images).
This technique allows the browser to select an optimal format for an image, for example a small image on a mobile
phone and a larger one, on a desktop.

The technique I use is based off of the works by 
[Laura Kalbag](https://laurakalbag.com/processing-responsive-images-with-hugo/), 
[Adam Wills](https://www.adamwills.io/blog/responsive-images-hugo/) and
[Nils Norman Haukås](https://nilsnh.no/2018/06/10/hugo-how-to-add-support-for-responsive-images-trough-image-processing-and-page-bundles-3/).

I use the same [Hugo Image Processing](https://gohugo.io/content-management/image-processing/) techniques as in other
parts of the [Hugo Chaschper](https://github.com/jcfischer/hugo-chaschper) template, this time in a 
[figure shortcut](https://github.com/jcfischer/hugo-chaschper/blob/master/layouts/shortcodes/figure.html) that 
overrides the Hugo internal one. 

It allows me to write 

```
{{</* figure src="/images/2019-01-19-size-before.png" alt="display of something" caption="A caption" */>}}
```

in my markdown files. From this, it generates the following code:

{{< highlight "html" >}}
<figure>
    <a href="https://invisible.ch/images/2019-01-19-size-before.png">
        <img
         srcset="
        /images/2019-01-19-size-before_hu..._320x0_resize_box_2.png 320w,
        /images/2019-01-19-size-before_hu..._600x0_resize_box_2.png 600w,
        /images/2019-01-19-size-before_hu..._1200x0_resize_box_2.png 1200w,
        /images/2019-01-19-size-before_hu..._1800x0_resize_box_2.png 2x"
        sizes="(max-width: 320px) 320w,
        (max-width: 600px) 600w,
        (max-width: 1200px) 1200w,
        2x"
        src="https://invisible.ch/images/2019-01-19-size-before_...3_1200x0_resize_box_2.png" alt="Website size before"/>
    </a>
    <figcaption><h4>A caption</h4></figcaption>
</figure>
{{< /highlight >}}

This give the browser a selection of 4 different images to display (in the `srcset` attribute) and a selection
of widths that allows the browser to select the correct one (via `sizes`). For browsers that don't support the `srcset/sizes` 
attribute, a medium sized image is selected. Finally, the whole image is wrapped in an `a` tag, that links to the original
image.

The code for the shortcut is not quite where I want it to be yet - it duplicates the actual code for generating the
`figure` tag, based on whether the image is pulled from the local Page bundle or from the static directory. As 
my Hugo templating foo improves, I will fix that duplication.

