---
layout: post
title: "define: Cloud Computing"
date: 2010-12-01
categories: ["PhD"]
tags: ["cloud", "definition", "scalability"]
author: "melmeric"
permalink: /2010/12/01/define-cloud-computing/
---

I have been looking for a good definition of Cloud Computing for a while. Cloud Computing is of course a **buzzword**, so no wonder its meaning is **fuzzy**. The [official definition of NIST](http://csrc.nist.gov/groups/SNS/cloud-computing/) reminds me of some standards: put everything together to make everyone happy.

Even [Wikipedia](http://en.wikipedia.org/wiki/Cloud_computing) gets a bit fuzzy about Cloud Computing, basically because it mixes up technical definitions, marketing, business models and a lot of other things. Also the critics do not help to define the thing, as they say things like "Cloud is everything we do" or "Technologies now dubbed as Cloud existed long before the name".

Given that a definition is always an *approximation* (ontologically, because it is just a categorization for our mind), the best technical definition (what I am interested in) I found was given in [this blog post](http://intotheinfrastructure.blogspot.com/2009/04/just-what-is-cloud-computing.html). I summarize it here **"Distributed location-independent scale-free cooperative agents"**. You can check the post to see what each piece of  the definition means.

While this was the best definition I found, it is not exactly what I have in mind when I think about Cloud Computing. Also, this does not encompass a lot of technologies that I can think of when I say Cloud (one for all, MapReduce). So I will take a stab at defining what Cloud Computing is:

**"Distributed, transparent, scale-free computing system"**

Yes, it doesn't change much, does it? But the core point here is that I do not care what kind of system we are talking about, but I just care that the system is distributed and scale-free. Furthermore location independence is not the only interesting property: access, failure and replication transparency are important as well. You should aim to the best transparency you can get without impacting performance (too much transparency hinders optimization).

The rationale is that a Cloud Computing is such that you can solve a problem faster/better just throwing more hardware at it. So **scalability** is the key feature, and in particular being **scale-free** (the scale of the system is not a design parameter).