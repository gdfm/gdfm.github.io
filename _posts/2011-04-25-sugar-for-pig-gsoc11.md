---
layout: "post"
title: "Sugar for Pig @ GSoC'11"
date: "2011-04-25 22:05:33"
last_modified_at: "2011-08-02 19:28:16"
author: "melmeric"
permalink: "/blog/2011/04/sugar-for-pig-gsoc11/"
categories:
  - "technology"
tags:
  - "cheers"
  - "gsoc"
  - "pig"
  - "syntactic-sugar"
comments: false
---

My proposal for this year's Google Summer of Code (GSoC) has been accepted!
Also this year I will be working on [Apache Pig](http://pig.apache.org/ "Apache Pig").
[Last year](/blog/2010/09/gsoc-wrap-up/) I worked on the backend and on improving performance. This year instead I will work on the front end and on improving usability. I will implement a couple of "[syntactic sugar](http://en.wikipedia.org/wiki/Syntactic_sugar)" features for Pig/Latin.

- Variable argument for SAMPLE and LIMIT. ([PIG-1926](https://issues.apache.org/jira/browse/PIG-1926 "PIG-1926"))
  Currently, SAMPLE and LIMIT only take a constant argument. It would be better to be able to use a variable (scalar) in the place of a constant.
- Default SPLIT destination. ([PIG-1904](https://issues.apache.org/jira/browse/PIG-1904 "PIG-1904"))
  SPLIT partitions a relation into two or more relations.
  It would be useful to have a default destination for tuples that are not assigned to any other relation, in a fashion similar to a switch/case/default statement.

These features are simple but quite useful. [My proposal](http://socghop.appspot.com/gsoc/proposal/review/google/gsoc2011/azaroth/1 "Sugar for Pig") outlines some interesting use cases.
This year I will be mentored by Thejas Nair. I am very happy to be able to contribute again to this very interesting open source project.
It's a pity I didn't start GSoCing before and this will be my last year (blame my memory, on my first year as a PhD student I missed the deadline by 3 days...).
