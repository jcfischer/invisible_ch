---
title: "Slimming"
date: 2019-01-19T12:02:45+01:00
author: "Jens-Christian Fischer"
description: "Reducing the weight of this blog"
image: "/images/2019-01-19-size-after.png"
categories: ["code"]
tags: ["hugo", "image", "resizing"]
language: en
slug:
type: post
---

[The Website Obesity Crisis](https://idlewords.com/talks/website_obesity.htm) is a wonderful talk about the sheer 
size that even simple websites have. Thanks to [@stilkov](https://twitter.com/stilkov) for the pointer:

2025-01-06: There used to be a link to twitter here, but somewhere in the last few years since I deployed my blog 
the twitter API changed/broke/whatever. I have therfore removed the content.


That led me to look at the size of this blog and it was scary:

{{< figure src="/images/2019-01-19-size-before.png" alt="Website size before">}}

The weight of the front page of this humble blog is a whopping 5 MB. When looking for the culprits, I came across 
two problematic areas:

* The small avatar image of myself bottom left (that is also shown on the [about](/about) page). It had a size
  of 4096x4096 pixels and was resized to 256 or 384 pixels square. I replaces it with a much smaller (256*256) sized 
  image and saved around 750 kb
* The other problematic area were the images shown for each article or blog post. I have started using images 
  for all articles, and I just pulled the full image in the preview. Obviously this is totally unnecessary.
  
I used the [Hugo Image Processing](https://gohugo.io/content-management/image-processing/) commands to generate
smaller sized images. I had to make one change to my `config.toml` file and add the `assetDir` directive. The
`assetDir` points to `static` where the images are stored in the `images` folder. That allows the image processing
directives to work on those assets as well (otherwise, they are limited to work on images stored in the same
[Page Bundle](https://gohugo.io/content-management/page-bundles/)) as the referencing code.

The code in my template looks like this:

{{< highlight "html" >}}
    {{if .Params.image}}
    {{ $img := resources.Get .Params.image }}
    {{ with $img }}
    <a class="post-card-image-link" href="{{ .Permalink }}">
        <div class="post-card-image" style="background-image: url({{ (.Fill "1200x600").Permalink }})"></div>
    </a>
    {{ end }}
    {{else}}
    ...
    {{{ end }}
{{< /highlight >}}    

Instead of the full image, I use a 1200x600 preview. (which is also used for the Facebook preview image).

Changing these simple things led to a drastic reduction of the overall page size: New 1.39MB (which is around
75% less). There still is room for improvement, but that will be the topic of another post.

{{< figure src="/images/2019-01-19-size-after.png" alt="Website size after">}}
