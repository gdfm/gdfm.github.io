---
layout: "post"
title: "Social Content Matching in MapReduce @ VLDB"
date: "2011-03-19 13:14:30"
last_modified_at: "2011-03-19 13:14:30"
author: "melmeric"
permalink: "/blog/2011/03/social-content-matching-in-mapreduce-vldb/"
categories:
  - "phd"
tags:
  - "content"
  - "graph"
  - "mapreduce"
  - "matching"
  - "paper"
  - "vldb"
  - "yahoo"
category_names:
  - "PhD"
tag_names:
  - "content"
  - "graph"
  - "mapreduce"
  - "matching"
  - "paper"
  - "vldb"
  - "Yahoo"
comments: false
sitemap: false
wp_id: 366
wp_slug: "social-content-matching-in-mapreduce-vldb"
permalink_slug: "social-content-matching-in-mapreduce-vldb"
wp_url: "https://gdfm.me/2011/03/19/social-content-matching-in-mapreduce-vldb/"
---

My last work *"Social Content Matching in MapReduce"* got accepted in VLDB
(Very Large Data Bases).
YES!!!
(as you might tell, I am extremely happy about this :) )
In the paper we tackle the problem of content distribution in a social media web site like flickr, model the problem as a b-matching problem on a graph and solve it with a smart iterative algorithm in MapReduce. We also show how to design a scalable greedy algorithm for the same problem in MapReduce.
Here the abstract:
> Matching problems are ubiquitous. They occur in economic markets, labor markets, internet advertising, and elsewhere. In this paper we focus on an application of matching for social media. Our goal is to distribute content from information suppliers to information consumers.
> We seek to maximize the overall relevance of the matched content from suppliers to consumers while regulating the overall activity, e.g., ensuring that no consumer is overwhelmed with data and that all suppliers have chances to deliver their content.
> We propose two matching algorithms, GreedyMR and StackMR, geared for the MapReduce paradigm. Both algorithms have provable approximation guarantees, and in practice they produce high-quality solutions. While both algorithms scale extremely well, we can show that StackMR requires only a poly-logarithmic number of MapReduce steps, making it an attractive option for applications with very large datasets. We experimentally show the trade-offs between quality and efficiency of our solutions on two large datasets coming from real-world social-media web sites.

On a final note, thanks to my co-authors for their hard work and guidance:
Aris Gionis from Yahoo! Research and Mauro Sozio from Max Planck Institut.
