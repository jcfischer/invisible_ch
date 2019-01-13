---
title: "Chaschper Galleries"
date: 2019-01-13T12:32:21+01:00
author: "Jens-Christian Fischer"
description: ""
image: "/images/2019-01-13-gallery.jpg"
categories: ["code"]
tags: ["hugo", "css"]
language: en
slug:
type: post
---

The new version of the [Chaschper](https://github.com/jcfischer/hugo-chaschper) template that I'm
using to power this blog has gained a new capability: Image galleries.

I started out with a [gallery by VickyLai](https://github.com/vickylai/hugo-theme-sam/blob/master/layouts/gallery/list.html) to see how to do that in 
general. From there I looked at [How to Build a Responsive Image Gallery with Flexbox](https://www.taniarascia.com/how-to-build-a-responsive-image-gallery-with-flexbox/) to do
some basic layouting and [Fluidbox](https://github.com/terrymun/Fluidbox) to style the images and load larger versions.
I didn't quite like the way, the galleries were defined in the original
example, so I came up with the following scheme:

My site can have multiple galleries, that each live in a directory under the `content/galleries` 
folder. All JPG images (for now) are included in the gallery. Finally, there is an `index.md`
file in the same folder that ties everything together. It looks like this

    ---
    title: "Scuol 2019-01-12"
    date: 2019-01-12T15:26:46+01:00
    tags: ["scuol", "winter"]
    type: "gallery"
    ---
    
    A wonderful, sunny day in Scuol. Pictures taken during a walk down to the Inn river. (iPhone Xs)

I use the [Page Resources](https://gohugo.io/content-management/page-resources/) in Hugo to create two smaller versions of each image (400 and 1200px) wide
for preview purposed (also because downloading 50MB of image data to show a gallery is - shall we
say - suboptimal). It took a bit of fiddling with the hugo templating language before things started to
work out. The relevant code in the [`layouts/gallery/single.html`](https://github.com/jcfischer/hugo-chaschper/blob/master/layouts/gallery/single.html) file look like this:

    <div class="photo-grid">
    {{- $resources := .Resources.Match "*.jpg"}}
    {{- range $resources }}
    {{- with . }}
        {{- $image400x := (.Resize "400x") }}
        {{- $image1200x := (.Resize "1200x") }}
        <a href="{{ $image1200x.RelPermalink }}" title="" class="photo-cell">
          <img src="{{ $image400x.RelPermalink }}"  alt="{{ .Name }}" title="" />
        </a>
    {{- end }}
    {{- end }}
    </div>

The code picks up the [Page Bundles](https://gohugo.io/content-management/page-bundles/) resources (i.e. all files that match "*.jpg"), iterates
over them and creates two new images. When Hugo builds the site, it will create those files
in the correct `public/galleries` directory and link correctly.

An example of one of these new galleries can be found here: [Sucol 2019-01-12](/galleries/2019-01-12/)

