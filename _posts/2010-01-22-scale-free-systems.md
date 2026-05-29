---
layout: "post"
title: "Scale-free systems"
date: "2010-01-22 12:08:20"
last_modified_at: "2010-01-22 12:08:20"
author: "melmeric"
permalink: "/blog/2010/01/scale-free-systems/"
categories:
  - "phd"
tags:
  - "scalability"
category_names:
  - "PhD"
tag_names:
  - "scalability"
comments: false
sitemap: false
wp_id: 40
wp_slug: "scale-free-systems"
permalink_slug: "scale-free-systems"
wp_url: "https://gdfm.me/2010/01/22/scale-free-systems/"
---

I have been looking around for the definition of **scale-free system** I came up with, I had totally forgotten where I took it from. I think I kind of ripped it from this [post](http://tdunning.blogspot.com/2009/01/real-time-decision-making-using-map.html) and condensed it into a concise form.
During the presentation I gave a couple of days ago I was asked if this scale-free had anything to do with *[scale-free networks](http://en.wikipedia.org/wiki/Scale-free_network), which are networks that follow a power-law in degree distribution (a few vertexes with high degree [Hubs] and a lot of vertexes with low degree). These networks are used as a model for Internet, social networks and a lot of other things. They have some interesting properties that are kept no matter the scale (number of nodes) of the network, and thus they exhibit self-similarity, fractal structure and the like.*
*My answer is: **no**.*
*Or at least, when I say scale-free I mean that the **scale is not a design parameter of the system**. Or alternatively that the system's design is free of scale, so you can run the system on 10 or 10^10 nodes without modification to the architecture. There might be some way so design a scale-free system using a power-law-distribution-of-something structure, but it is not the main point.*
