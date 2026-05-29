---
layout: "post"
title: "Numbers everyone should know"
date: "2010-06-11 18:16:02"
last_modified_at: "2012-08-03 12:05:48"
author: "melmeric"
permalink: "/blog/2010/06/numbers-everyone-should-know/"
categories:
  - "phd"
  - "technology"
tags:
  - "cache"
  - "disk"
  - "memory"
  - "numbers"
  - "performance"
  - "reference"
category_names:
  - "PhD"
  - "Technology"
tag_names:
  - "cache"
  - "disk"
  - "memory"
  - "numbers"
  - "performance"
  - "reference"
comments: false
sitemap: false
wp_id: 116
wp_slug: "numbers-everyone-should-know"
permalink_slug: "numbers-everyone-should-know"
wp_url: "https://gdfm.me/2010/06/11/numbers-everyone-should-know/"
---

I was watching Jeff Dean's [keynote presentation for the ACM Symposium on Cloud Computing 2010](http://hosted.mediasite.com/mediasite/Viewer/?peid=1330ca0a008f4394917c2b7eb3163f1b1d "Jeff Dean Keynote SOCC 2010") (SOCC) that was held yesterday and I found this very interesting bit of information. This is so useful that every Computer Scientist and Engineer should learn it by heart!
<table style="height:264px;" width="357" border="1">
<tbody>
<tr>
<td><strong>Operation</strong></td>
<td><strong>Time (nsec)</strong></td>
</tr>
<tr>
<td>L1 cache reference</td>
<td>0.5</td>
</tr>
<tr>
<td>Branch mispredict</td>
<td>5</td>
</tr>
<tr>
<td>L2 cache reference</td>
<td>7</td>
</tr>
<tr>
<td>Mutex lock/unlock</td>
<td>25</td>
</tr>
<tr>
<td>Main memory reference</td>
<td>100</td>
</tr>
<tr>
<td>Compress 1KB bytes with Zippy</td>
<td>3,000</td>
</tr>
<tr>
<td>Send 2K bytes over 1 Gbps network</td>
<td>20,000</td>
</tr>
<tr>
<td>Read 1MB sequentially from memory</td>
<td>250,000</td>
</tr>
<tr>
<td>Roundtrip within same datacenter</td>
<td>500,000</td>
</tr>
<tr>
<td>Disk seek</td>
<td>10,000,000</td>
</tr>
<tr>
<td>Read 1MB sequentially from disk</td>
<td>20,000,000</td>
</tr>
<tr>
<td>Send packet CA -&gt; Netherlands -&gt; CA</td>
<td>150,000,000</td>
</tr>
</tbody>
</table>
These numbers give you some insight into why random reads from a disk are a **really bad** idea.
This piece information complements the very nice image from Adam Jacobs, and his excellent "[The Pathologies of Big Data](http://queue.acm.org/detail.cfm?id=1563874 "on ACM Queue, by Adam Jacobs")" article.
[![Comparison of random and sequential speeds for Memory, SSD and Disk](http://deliveryimages.acm.org/10.1145/1570000/1563874/jacobs3.jpg "Memory VS SSD VS Disk")](http://queue.acm.org/detail.cfm?id=1563874) Random is BAD (and SSD is NOT going to solve the problem)
What should we learn from all this stuff?

- Do your back-of-the-envelope calculations
- Do avoid random operations
- Do benchmarks your system
