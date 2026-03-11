---
layout: post
title: "GSoC 2012: the other side of the fence"
date: 2012-05-24
categories: ["Research", "Technology"]
tags: ["GSoC", "mentor", "pig", "rank"]
author: "melmeric"
permalink: /2012/05/24/gsoc-2012-the-other-side-of-the-fence/
---

And here it comes again as every year, [Google Summer of Code](http://code.google.com/soc/)!

As usual, I will be working for [Apache Pig](http://pig.apache.org) also this summer. However, I will be working from the other side of the fence this time: I will be mentoring!

As I have already graduated and I am no more a student (shock!) I cannot take part as a student (no way!). So I decided to mentor.

	
- Pro: you need much less time to mentor compared to being a student.
	
- Con: you don't learn as much, nor have as much fun, nor get the same recognition, nor get paid as much. ;)

However, the great thing about mentoring is that you propose ideas you would like to see realized in the project, and then students make them real!
Indeed, the project I am mentoring this year is about an idea I had some while ago.
It happens very often (to me and to my colleagues as well) to have a list of tuples and to need to attach a unique number to it.
For example when creating the lexicon for a collection of documents you have a list of unique words appearing in the collection, and you want to transform each word into a numerical id to reduce memory usage and ease later processing.

A while ago I implemented a MapReduce algorithm for this task that scales very well (i.e. no single reducer that does all the work).
However this same problem comes up very often and it is cumbersome to fit a MR job in the middle of a Pig pipeline while you are building the script in an iterative way (read: you don't know what you are doing), especially because the code I wrote is not general enough to be applied as is, so each time I need to customize it a bit.
"Indeed, why the hell Pig does not do it already?"  was my reaction. So [PIG-2353](https://issues.apache.org/jira/browse/PIG-2353) was born.

[PIG-2353](https://issues.apache.org/jira/browse/PIG-2353) is quite a stretch for a night's coding, so it stayed there for a while. Until an interested student got interested in it for GSoC. Enter Allan Avendaño.

You can follow Allan's progress also on [his blog](http://blog.espol.edu.ec/xallam/).
He has already got his first patch in ([PIG-2583](https://issues.apache.org/jira/browse/PIG-2583)) and started working on the main project this week.
I expect great stuff coming out of this project!

I am ready for a great summer, "flipping bits not burgers".