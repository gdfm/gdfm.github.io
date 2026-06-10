---
layout: "post"
title: "How to run a MiniCluster based JUnit test with Eclipse"
date: "2010-08-03 22:10:00"
last_modified_at: "2011-01-03 15:21:06"
author: "melmeric"
permalink: "/blog/2010/08/how-to-run-a-minicluster-based-junit-test-with-eclipse/"
categories:
  - "technology"
tags:
  - "cloud"
  - "gsoc"
  - "junit"
  - "mapreduce"
  - "pig"
comments: false
---

Here is a little trick I had to learn while developing Apache Pig.
Pig uses JUnit as test framework. JUnit tests are very useful for unit testing, but end-to-end testing is not as easy. Even more in the case of Pig, that uses [Hadoop](http://hadoop.apache.org/ "Hadoop") (a distributed MapReduce engine) to execute its scripts. The `MiniCluster` class addresses this issue: it simulates a full execution environment on the local machine, with HDFS and everything you need. More information [here](http://wiki.apache.org/pig/HowToContribute "How to contribute to Pig").
`MiniCluster` is very easy to use, assuming you are running your tests via ant. But if you want to debug and trace your test (using Eclipse, for instance) there are a couple of catches. Basically, you need to reproduce the environment the ant script builds inside Eclipse.
The first thing to set is the `hadoop.log.dir` property, that tells where to put logs. Its default value is `build/test/logs`. To set it, go in the Run Configurations screen, Arguments tab, and add this line to the VM arguments:
@@WXR\_RAW\_BLOCK\_0@@
If you forget to set this, you will get a nice NullPonterException:
@@WXR\_RAW\_BLOCK\_1@@
The other thing to take care of is where to find `MiniCluster`'s configuration file. For Pig, you should first create it by running the `ant test` target once from the command line. This will create a standard minimum configuration file for your use in `${HOME}/pigtest/conf`. To set it, you should add this directory to the classpath in the Classpath tab, under User Entries using the Advanced... button.
If you forget to set this, you get a nice `ExecException`:
@@WXR\_RAW\_BLOCK\_2@@
Even after this, you will still get some exceptions (regarding threads, manifest files, jars), but they are not a problem and debugging will work.
Hope this helps!
