---
title:  "Greenifying the blog"
date:   2023-01-06 01:00:00 +0100
categories: "general"
description: "Long live WebP!"
---

You can call me a hipster, but this blog was meant to be “green” ever since the beginning. By that I mean that it should be minimal, simple and quick to load. Over time, though, I got carried away with my pretty nice camera and obsession with taking pictures of circuit boards, which led to the site taking up almost 100MB, which I could not accept for a blog with some images. Thus, I looked into ways to make it smaller. 

One of the first techniques I found, which I had never considered before, was to convert all images from JPG/PNG to WebP. Sources on the internet stated that this would result in a 25-34% decrease in file size, which would have been quite nice, since all I’d need to do is run a simple script and then replace all occurrences of JPG/PNG in the HTML with WebP. I was definitely not prepared for what I got.

<figure>
<img src="{{ site.baseurl }}/images/compression_example.webp" alt="Image of the size decrease" style="display:block;margin:auto;">
<figcaption style="text-align:center"><i>Not only does WebP look better, but it's much smaller as well</i></figcaption>
</figure>

Before running the script, all of the images took up 64.9MB. After the script? 12.4MB. That’s not 25-34% decrease, that’s 81%! (this blog post was delayed due to the temporary death of my TI-84 Plus Silver Edition calculator, without which I couldn’t do this calculation, and it turns out that one of the batteries in it went negative, which [can actually happen under specific conditions](https://www.panasonic-batteries.com/en/faq/why-does-battery-show-minus-voltage-when-checked-voltmeter)) This is great for my blog and a tip for everyone else who wants to do blogs. Both relevant browsers (Chrome and Firefox) support WebP nowadays, and I believe that reducing file size for the 99% of internet users is much more important than supporting those with archaic browsers.

<figure>
<img src="{{ site.baseurl }}/images/compression_example_2.webp" alt="Image of the file size decrease of the previous image" style="display:block;margin:auto;">
<figcaption style="text-align:center"><i>Even this image decreased from 181KB to 39KB when converted</i></figcaption>
</figure>

Google releases and offers documentation for WebP conversion tools. You can download the [whole WebP suite here](https://storage.googleapis.com/downloads.webmproject.org/releases/webp/index.html).
You can look at the documentation [here (the relevant file for conversion to WebP is cwebp.exe)](https://developers.google.com/speed/webp/docs/using).
To batch convert to WebP, you can use [this script (among others)](https://github.com/kasipavankumar/batch-conversion-to-webp).