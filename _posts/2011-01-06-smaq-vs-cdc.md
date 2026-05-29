---
layout: "post"
title: "SMAQ vs CDC"
date: "2011-01-06 04:11:08"
last_modified_at: "2011-01-06 19:10:31"
author: "melmeric"
permalink: "/blog/2011/01/smaq-vs-cd/"
categories:
  - "phd"
tags:
  - "category"
  - "cloud"
  - "mapreduce"
  - "oreilly"
  - "proposal"
  - "stack"
  - "systems"
category_names:
  - "PhD"
tag_names:
  - "category"
  - "cloud"
  - "mapreduce"
  - "oreilly"
  - "proposal"
  - "stack"
  - "systems"
comments: false
sitemap: false
wp_id: 216
wp_slug: "smaq-vs-cd"
permalink_slug: "smaq-vs-cd"
wp_url: "https://gdfm.me/2011/01/06/smaq-vs-cd/"
---

The name SMAQ (Storage MapReduce And Query) Cloud Stack was proposed by Edd Dumbill in [this article](http://radar.oreilly.com/2010/09/the-smaq-stack-for-big-data.html) on O'Reilly Radar (the article is sure worth reading).
While I find that a nice name is a good way to crystallize a concept, I am not sure it captures the whole picture about Big Data.
For example, compare the image on the left from the article, with the one on the right that comes directly from my [Ph.D. research proposal](/blog/2010/02/phd-thesis-proposal/).
[![The SMAQ stack for Big Data](http://radar.oreilly.com/upload/2010/09/smaq-overview-m.png "SMAQ")](http://radar.oreilly.com/2010/09/the-smaq-stack-for-big-data.html)

[![Cloud Computing Stack](/assets/media/2010/12/cloud-architecture.png "cloud-architecture")](/assets/media/2010/12/cloud-architecture.png)
I will now dub my stack proposal CDC (Computation Data Coordination) stack (suggestions for better names super welcome!).
The query layer from SMAQ would map to my High Level Languages layer.
This layer includes systems like Pig, Hive and Cascading.
The MapReduce layer from SMAQ would map to my Computation layer.
The only other system in this layer is Dryad, for the moment, but there could be many others.
The Storage layer from SMAQ would map to my Distributed Data layer.
The SMAQ classification does not differentiate between systems like HDFS and HBase.
According to me, the high level interface is what distinguishes HDFS from HBase (or for example Voldemort from Cassandra).
That is why I would put HDFS and Voldemort in the Distributed Data layer, and HBase and Cassandra in the Data Abstraction layer (even though Cassandra does not actually rely on another system to store its data).
Finally, the SMAQ stack is totally lacking the Coordination layer.
This is comprehensible, as the audience of radar is more "analyst" oriented. From a operational perspective, systems like Chubby and Zookeeper are useful to build the frameworks in the stack.
What is missing from both stacks, and will be the main trend in 2011, is the Real-Time layer (even though I would have no idea where to put it :) )
