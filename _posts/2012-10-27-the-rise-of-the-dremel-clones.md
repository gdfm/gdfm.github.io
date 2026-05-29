---
layout: "post"
title: "The rise of the Dremel clones"
date: "2012-10-27 04:41:21"
last_modified_at: "2012-10-27 04:41:21"
author: "melmeric"
permalink: "/blog/2012/10/the-rise-of-the-dremel-clones/"
categories:
  - "technology"
tags:
  - "apache"
  - "big-data"
  - "cloudera"
  - "dremel"
  - "drill"
  - "druid"
  - "google"
  - "hadoop"
  - "impala"
  - "mapreduce"
  - "open-source"
  - "real-time-analytics"
category_names:
  - "Technology"
tag_names:
  - "Apache"
  - "big data"
  - "Cloudera"
  - "dremel"
  - "drill"
  - "druid"
  - "Google"
  - "hadoop"
  - "impala"
  - "mapreduce"
  - "open source"
  - "real-time analytics"
comments: false
sitemap: false
wp_id: 863
wp_slug: "the-rise-of-the-dremel-clones"
permalink_slug: "the-rise-of-the-dremel-clones"
wp_url: "https://gdfm.me/2012/10/27/the-rise-of-the-dremel-clones/"
---

It looks like people are now realizing the need for powerful real-time analytics engines. [Dremel](http://research.google.com/pubs/pub36632.html "Dremel") was designed by Google as an interactive query engine for cluster environments. Dremel is a scalable, interactive ad-hoc query system for analysis of read-only nested data. It's the perfect tool to power your Big Data dashboards. Now a bunch of open source clones are appearing. Will they have the same luck as Hadoop?
Here the contenders:

- The regular: [Apache Drill](http://incubator.apache.org/drill/ "Drill")
  Mainly supported by MapR Technologies and currently in incubator. At the moment of writing there are a total of 12 issues in Jira (for a comparison, we just got to 3000 in Pig this week). Even the name [still needs to be confirmed](https://issues.apache.org/jira/browse/DRILL-12). As usual in the Apache style, this will most likely be a community-driven project, with all the pros and cons of the case. The Java + Maven + Git combo should be familiar and enable contributors to get up to speed quickly.
- The challenger: [Cloudera Impala](https://github.com/cloudera/impala "Impala")Just open-sourced [a couple of days ago](http://blog.cloudera.com/blog/2012/10/cloudera-impala-real-time-queries-in-apache-hadoop-for-real/). Surprisingly, it even offers the possibility of joining tables (something Dremel didn't do for efficiency reasons). Unfortunately it is all C++, which I have hanged on the nail after my master's thesis. I hope this choice won't scare away contributors. However I suspect that Cloudera wants to drive most of the development in-house rather than build a community project.
- The outsider: [Metamarkets Druid](http://metamarkets.com/druid/ "Druid")Even though it has [been around for a year](http://metamarkets.com/2011/druid-part-i-real-time-analytics-at-a-billion-rows-per-second/), it has only [recently become open source](http://metamarkets.com/2012/metamarkets-open-sources-druid/). It's interesting to read how these guys were frustrated by existing technology so they just decided to roll their own solution. My (unsupported) feeling is that this is by far the most mature of the three clones. One interesting feature of Druid is real-time ingestion of data. From what I gather, Impala relies on Hive tables and Drill on Avro files, so my guess is that both of them cannot do the same. (For the records, also here Java + Maven + Git).

As a technical side note, and a personal curiosity, I wonder whether these project would benefit from YARN integration. I guess it will be easier for Drill than for the others. However startup latency could be an issue in this case.
The whole situation seems like a déjà vu of the Giraph/Hama/GoldenOrb clones of Pregel. Who will win the favor of the Big Data crowd?
Who will be able to grow the largest community? Technical issues are only a part of the equation in this case.
I am quite excited to see this missing piece of the Big Data ecosystem getting more attention and thrilled by the competition.
**PS**: I have read somewhere around the Web that this will be the end of Hadoop and MapReduce. Nothing can be more wrong than this idea. Dremel is the perfect complement for MapReduce. Indeed, how better could you analyze the results of you MapReduce computation? Often the results are at least as big as the inputs, so you need a way to quickly generate small summaries. Hadoop counters have been (ab)used for this purpose, but more flexible and powerful post-processing capabilities are needed.
**PPS**: Just to be clear, there is nothing tremendously innovative in the science behind these products. Distributed query execution engines have been around for a while in parallel database systems. What's yet to see is whether they can deliver their promise of extreme scalability, which parallel database system have failed to offer.
