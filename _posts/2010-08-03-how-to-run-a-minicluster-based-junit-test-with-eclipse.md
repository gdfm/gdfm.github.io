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
category_names:
  - "Technology"
tag_names:
  - "cloud"
  - "GSoC"
  - "junit"
  - "mapreduce"
  - "pig"
comments: false
sitemap: false
wp_id: 118
wp_slug: "how-to-run-a-minicluster-based-junit-test-with-eclipse"
permalink_slug: "how-to-run-a-minicluster-based-junit-test-with-eclipse"
wp_url: "https://gdfm.me/2010/08/03/how-to-run-a-minicluster-based-junit-test-with-eclipse/"
---

Here is a little trick I had to learn while developing Apache Pig.
Pig uses JUnit as test framework. JUnit tests are very useful for unit testing, but end-to-end testing is not as easy. Even more in the case of Pig, that uses [Hadoop](http://hadoop.apache.org/ "Hadoop") (a distributed MapReduce engine) to execute its scripts. The `MiniCluster` class addresses this issue: it simulates a full execution environment on the local machine, with HDFS and everything you need. More information [here](http://wiki.apache.org/pig/HowToContribute "How to contribute to Pig").
`MiniCluster` is very easy to use, assuming you are running your tests via ant. But if you want to debug and trace your test (using Eclipse, for instance) there are a couple of catches. Basically, you need to reproduce the environment the ant script builds inside Eclipse.
The first thing to set is the `hadoop.log.dir` property, that tells where to put logs. Its default value is `build/test/logs`. To set it, go in the Run Configurations screen, Arguments tab, and add this line to the VM arguments:
<pre>
-Dhadoop.log.dir=build/test/logs
</pre>
If you forget to set this, you will get a nice NullPonterException:
<pre>ERROR mapred.MiniMRCluster: Job tracker crashed
java.lang.NullPointerException
at java.io.File.&lt;init&gt;(File.java:222)
at org.apache.hadoop.mapred.JobHistory.init(JobHistory.java:151)
at org.apache.hadoop.mapred.JobTracker.&lt;init&gt;(JobTracker.java:1617)
at org.apache.hadoop.mapred.JobTracker.startTracker(JobTracker.java:183)
at org.apache.hadoop.mapred.MiniMRCluster$JobTrackerRunner.run(MiniMRCluster.java:106)
at java.lang.Thread.run(Thread.java:619)</pre>
The other thing to take care of is where to find `MiniCluster`'s configuration file. For Pig, you should first create it by running the `ant test` target once from the command line. This will create a standard minimum configuration file for your use in `${HOME}/pigtest/conf`. To set it, you should add this directory to the classpath in the Classpath tab, under User Entries using the Advanced... button.
If you forget to set this, you get a nice `ExecException`:
<pre>org.apache.pig.backend.executionengine.ExecException: ERROR 4010: Cannot find hadoop configurations in 
 classpath (neither hadoop-site.xml nor core-site.xml was found in the classpath).If you plan to use 
 local mode, please put -x local option in command line
 at org.apache.pig.backend.hadoop.executionengine.HExecutionEngine.init(HExecutionEngine.java:149)
 at org.apache.pig.backend.hadoop.executionengine.HExecutionEngine.init(HExecutionEngine.java:114)
 at org.apache.pig.impl.PigContext.connect(PigContext.java:183)
 at org.apache.pig.PigServer.&lt;init&gt;(PigServer.java:216)
 at org.apache.pig.PigServer.&lt;init&gt;(PigServer.java:205)
 at org.apache.pig.PigServer.&lt;init&gt;(PigServer.java:201)
 at org.apache.pig.test.TestSecondarySort.setUp(TestSecondarySort.java:73)
 at sun.reflect.NativeMethodAccessorImpl.invoke0(Native Method)
 at sun.reflect.NativeMethodAccessorImpl.invoke(NativeMethodAccessorImpl.java:39)
 at sun.reflect.DelegatingMethodAccessorImpl.invoke(DelegatingMethodAccessorImpl.java:25)
 at java.lang.reflect.Method.invoke(Method.java:597)
 at org.junit.runners.model.FrameworkMethod$1.runReflectiveCall(FrameworkMethod.java:44)
 at org.junit.internal.runners.model.ReflectiveCallable.run(ReflectiveCallable.java:15)
 at org.junit.runners.model.FrameworkMethod.invokeExplosively(FrameworkMethod.java:41)
 at org.junit.internal.runners.statements.RunBefores.evaluate(RunBefores.java:27)
 at org.junit.internal.runners.statements.RunAfters.evaluate(RunAfters.java:31)
 at org.junit.runners.BlockJUnit4ClassRunner.runChild(BlockJUnit4ClassRunner.java:73)
 at org.junit.runners.BlockJUnit4ClassRunner.runChild(BlockJUnit4ClassRunner.java:46)
 at org.junit.runners.ParentRunner.runChildren(ParentRunner.java:180)
 at org.junit.runners.ParentRunner.access$000(ParentRunner.java:41)
 at org.junit.runners.ParentRunner$1.evaluate(ParentRunner.java:173)
 at org.junit.internal.runners.statements.RunBefores.evaluate(RunBefores.java:28)
 at org.junit.internal.runners.statements.RunAfters.evaluate(RunAfters.java:31)
 at org.junit.runners.ParentRunner.run(ParentRunner.java:220)
 at org.eclipse.jdt.internal.junit4.runner.JUnit4TestReference.run(JUnit4TestReference.java:49)
 at org.eclipse.jdt.internal.junit.runner.TestExecution.run(TestExecution.java:38)
 at org.eclipse.jdt.internal.junit.runner.RemoteTestRunner.runTests(RemoteTestRunner.java:467)
 at org.eclipse.jdt.internal.junit.runner.RemoteTestRunner.runTests(RemoteTestRunner.java:683)
 at org.eclipse.jdt.internal.junit.runner.RemoteTestRunner.run(RemoteTestRunner.java:390)
 at org.eclipse.jdt.internal.junit.runner.RemoteTestRunner.main(RemoteTestRunner.java:197)</pre>
Even after this, you will still get some exceptions (regarding threads, manifest files, jars), but they are not a problem and debugging will work.
Hope this helps!
