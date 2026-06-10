---
layout: "post"
title: "BSP with Hadoop (and without) "
date: "2011-11-19 19:12:17"
last_modified_at: "2011-11-19 19:14:37"
author: "melmeric"
permalink: "/blog/2011/11/bsp-with-hadoop-and-without/"
categories:
  - "phd"
  - "technology"
tags:
  - "cloud"
  - "giraph"
  - "graph"
  - "hadoop"
  - "hama"
  - "programming"
comments: false
---

I have recently started to look at the [BSP (Bulk Synchronous Parallel)](http://en.wikipedia.org/wiki/Bulk_Synchronous_Parallel) model of computation for large scale graph analysis.
The model itself is quite old, but it has seen a resurgence lately mainly because of the [Pregel](http://googleresearch.blogspot.com/2009/06/large-scale-graph-computing-at-google.html) system by Google. Here the [paper](http://kowshik.github.com/JPregel/pregel_paper.pdf).
The idea of Pregel is to use synchronous barriers to cleanly separate messages in rounds.
In each step, a vertex can read the messages sent to it in the previous step, perform some computation, and generate messages for the next step.
When all the nodes vote to halt the  algorithm and no more messages arrive, the computation stops.

As with MapReduce and Hadoop, a number of clones of Pregel have popped up.
I will briefly review the most interesting ones in this post.

[Apache Giraph](https://github.com/aching/Giraph)

Giraph is a Hadoop-based graph processing engine open sourced by Yahoo! and now in the Apache Incubator.
It is at a very early stage, but the community looks very active and diverse. Giraph developers play in the same backyard of Hadoop, Pig and Hive developers, and this makes me feel confident about its future.
Giraph uses Hadoop for scheduling its workers and get the data loaded in memory, but then implements its own communication protocol using HadoopRPC. It also uses Zookeeper for fault tolerance by periodic checkpointing.
Interestingly, Giraph does not require installing anything on the cluster, so you can try it out on your existing Hadoop infrastructure. A Giraph job runs like a normal map-only job. It can actually be thought as a graph-specific Hadoop library.
However, because of this fact, the API currently lack encapsulation. Users need to write a custom  Reader + Writer + InputFormat + OutputFormat for each Vertex program they create. A library to read common graph formats would be a nice addition.

**The good:**
Very active community with people from the Hadoop ecosystem.
Runs directly on Hadoop.

**The bad:**
Early stage.

Hadoop leaks in the API.

[Apache Hama](https://github.com/aching/Giraph)

Hama is a Hadoop-like solution and is the oldest member in the group. Currently it is in the Apache Incubator and it was initially developed by an independent Korean programmer.
Hama focuses on general BSP computations, so it is not only for graphs. For example there are algorithms for matrix inversion and linear algebra (I know, one could argue that a graph and a matrix are actually the same data structure).
Unfortunately, the project seems to be moving slowly even though lately there has been a spike of activity, probably caused mainly by the GSoC (it works!).
Currently it is still at a **very** early stage:  the current version doesn't provide a proper I/O API and data partitioner. From my understanding there is no fault-tolerance either.
From the technical point of view, Hama uses Zookeeper for  coordination and HDFS for data persistence. It is designed to be "The Hadoop of BSP".
Given its focus on general BSP, the kind of primitives that it provides are at a low level of abstraction, very much like a restricted version of MPI.

**The good:**
General BSP.
Complete system.
The [logo](http://incubator.apache.org/hama/images/hama_paint_logo.png) is cute.

**The bad:**
Early stage.
Requires additional infrastructure.
Graph processing library not yet released.

[GoldenOrb](http://www.goldenorbos.org/)

GoldenOrb is a Hadoop based Pregel clone open sourced by Ravel. It should be in the process of getting into the Apache Incubator.
It is a close clone of Pregel and very similar to Giraph: a system to run distributed iterative algorithms on graphs.
The components of the system like vertex values (state), edges and messages are built on top of the Hadoop Writables system.
One thing I don't understand is why they didn't leverage Java generics. To get the value of a message you need to do ugly explicit casts:
<pre><code>@Override public void compute(Collection&lt;IntMessage&gt; messages) </code>{
  int _maxValue = 0;
  for(IntMessage m: messages) {
    int msgValue = ((IntWritable)m.getMessageValue()).get();
    _maxValue = Math.max(_maxValue, msgValue);
  }
}</pre>
As with Giraph, Hadoop details leak into the API. However, GoldenOrb requires additional infrastructure to run. An OrbTracker needs to be running on each Hadoop node. It Also uses HadoopRPC for communication. The administrator can define the number of partitions to assign to each OrbTracker and the threads per node to launch can be configured on a per-job basis.

**The good:**
Commercial support.

**The bad:**
Early stage, not yet in Incubator.
API has rough edges.
Requires additional infrastructure.

[JPregel](http://kowshik.github.com/JPregel)

A final mention goes to JPregel. It is a Java clone of Pregel which is **not** Hadoop based.
The programming interface is thought from the ground up and is very clean.
Right now it is at a **very very** early stage of development, e.g. messages can only be doubles and the system itself is not yet finalized.
Interestingly, no explicit halting primitive is present. From what I understood it automatically deduces the termination by the absence of new messages.
It is a very nice piece of work, especially considering the fact that it has been done by only a couple of first year master students.

PS: I waited too much before publishing this post and I was beaten on time by one of the Giraph committers, even though he reviews also some other piece of software. Have a look at his [post](http://blog.acaro.org/entry/google-pregel-the-rise-of-the-clones).
