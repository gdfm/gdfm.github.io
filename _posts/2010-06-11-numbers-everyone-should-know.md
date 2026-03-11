---
layout: post
title: "Numbers everyone should know"
date: 2010-06-11
categories: ["PhD", "Technology"]
tags: ["cache", "disk", "memory", "numbers", "performance", "reference"]
author: "melmeric"
permalink: /2010/06/11/numbers-everyone-should-know/
---

I was watching Jeff Dean's [keynote presentation for the ACM Symposium on Cloud Computing 2010](http://hosted.mediasite.com/mediasite/Viewer/?peid=1330ca0a008f4394917c2b7eb3163f1b1d) (SOCC) that was held yesterday and I found this very interesting bit of information. This is so useful that every Computer Scientist and Engineer should learn it by heart!

**Operation**
**Time (nsec)**

L1 cache reference
0.5

Branch mispredict
5

L2 cache reference
7

Mutex lock/unlock
25

Main memory reference
100

Compress 1KB bytes with Zippy
3,000

Send 2K bytes over 1 Gbps network
20,000

Read 1MB sequentially from memory
250,000

Roundtrip within same datacenter
500,000

Disk seek
10,000,000

Read 1MB sequentially from disk
20,000,000

Send packet CA -> Netherlands -> CA
150,000,000

These numbers give you some insight into why random reads from a disk are a **really bad** idea.

This piece information complements the very nice image from Adam Jacobs, and his excellent "[The Pathologies of Big Data](http://queue.acm.org/detail.cfm?id=1563874)" article.

[caption id="" align="alignnone" width="468"]![Comparison of random and sequential speeds for Memory, SSD and Disk](http://deliveryimages.acm.org/10.1145/1570000/1563874/jacobs3.jpg)[](http://queue.acm.org/detail.cfm?id=1563874) Random is BAD (and SSD is NOT going to solve the problem)[/caption]

What should we learn from all this stuff?

	
- Do your back-of-the-envelope calculations
	
- Do avoid random operations
	
- Do benchmarks your system