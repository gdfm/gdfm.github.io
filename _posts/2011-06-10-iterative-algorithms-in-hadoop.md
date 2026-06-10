---
layout: "post"
title: "Iterative algorithms in Hadoop"
date: "2011-06-10 20:05:27"
last_modified_at: "2011-07-25 21:43:16"
author: "melmeric"
permalink: "/blog/2011/06/iterative-algorithms-in-hadoop/"
categories:
  - "phd"
tags:
  - "algorithm"
  - "hadoop"
  - "iterative"
  - "mapreduce"
comments: false
---

While speaking about [my latest work](/blog/2011/03/social-content-matching-in-mapreduce-vldb/ "Social Content Matching in MapReduce") with some researchers, they confessed me they were very curious about how to implement an iterative algorithm in MapReduce/Hadoop. They made me realize that the task is not exactly straightforward, so I decided to write a post about it, and here we are.
The general idea for iterative algorithms in MapReduce is to chain multiple jobs together, using the output of the last one as the input of the next one. An important consideration is that, given the usual size of the data, the termination condition must be computed within the MapReduce program. The standard MapReduce model does not offer simple elegant ways to do this, but Hadoop has some added features that simplify this task: [Counters](http://philippeadjiman.com/blog/2010/01/07/hadoop-tutorial-series-issue-3-counters-in-action/ "A simple tutorial on counters").
To check for a termination condition with Hadoop counters, you run the job and collect statistics while its running. Then you access the counters and get their values, you might also compute derivate measures from counters and finally decide whether to continue iterating or to stop.
Here an example. The code is only partial, it's intended just to show the technique. Suppose we want to do some directed graph processing using a diffusion process (the exact application doesn't matter, I am using a coloring example here). Assume the mapper propagates the information along the graph and the reducer computes the new one.
@@WXR\_RAW\_BLOCK\_0@@
In this snippet, we scan the incoming edges for each vertex and compute the number of edges for each color. Then we proceed to compute the new color based on some procedure (omitted for brevity) and write the updated results.
After the scan, we use the counters to report how many edges of each color we have seen. At the end of the job we will have a global view of the colors in the graph.
If we update the vertex with a new color, we report it using another counter (UPDATED). At the end of the job this counter will tell us how many updates have been performed during this round.
Now suppose we want to run this algorithm up to stabilization, that is up to the point where no more updates will occur. To do this, we can simply check the number of updates reported by the counter and stop when it reaches zero. This must be done in the driver program, in between successive invocations of the MapReduce job.
Another important thing for an iterative algorithm in Hadoop is defining a naming schema for the iterations. The simplest thing is to create a working directory based on the input or output name. Every iteration will use a directory inside the working directory for input and output.
@@WXR\_RAW\_BLOCK\_1@@
This snippet shows the driver program, usually realized by implementing the org.apache.hadoop.util.Tool interface and overriding the run() method. In the first part the driver interacts with the file system to create the working directory. Then we launch our first job which serves a double purpose, it copies the input in the working directory and performs any initial preprocessing needed. Finally, in the third part we start our iterations.
For each job, the input is the output of the last run. The output goes into the working directory with an increasing counter added at the end. After the job finishes we remove the temporary files (this is useful if we perform many iterations with many reducers and we have quotas on the namenode). We also access the counters to print a summary view of the graph and to compute the termination condition.
That's it. Not too complicated after all :)
