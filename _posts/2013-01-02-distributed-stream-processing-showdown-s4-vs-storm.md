---
layout: "post"
title: "Distributed stream processing showdown: S4 vs Storm"
date: "2013-01-02 12:00:10"
last_modified_at: "2013-01-09 13:01:33"
author: "melmeric"
permalink: "/blog/2013/01/distributed-stream-processing-showdown-s4-vs-storm/"
categories:
  - "research"
  - "technology"
tags:
  - "big-data"
  - "distributed-systems"
  - "s4"
  - "showdown"
  - "storm"
  - "stream-processing"
comments: false
---

S4 and Storm are two distributed, scalable platforms for processing continuous unbounded streams of data.

I have been involved in the development of S4 (I designed the fault-recovery module) and I have used Storm for my latest project, so I have gained a bit of experience on both and I want to share my views on these two very similar and competing platforms.

First, some commonalities.
Both are distributed stream processing platforms, run on the JVM (S4 is pure Java while Storm is part Java part Clojure), are open source (Apache/Eclipse licenses), are inspired by MapReduce and are quite new. Both frameworks use keyed streams as their basic building block.

Now for some differences.

### Programming model.

S4 implements the Actors programming paradigm. You define your program in terms of Processing Elements (PEs) and Adapters, and the framework instantiates one PE per each unique key in the stream. This means that the logic inside a PE can be very simple, very much like MapReduce.

Storm does not have an explicit programming paradigm. You define your program in terms of bolts and spouts that process partitions of streams. The number of bolts to instantiate is defined a-priori and each bolt will see a partition of the stream.

To make things more clear, let's use the classic "hello world" program from MapReduce: word count.

Let's say we want to implement a streaming word count. In S4, we can define a word to be a key, and our PE would need to keep track of the number of instances it processes by using a single long (again, very much like MapReduce). In Storm, we need to program each bolt as if it had to process the whole stream, so we would use a data structure like a Map<String, Long> to keep track of the word counts. The distribution and parallelism are orthogonal to the program.

In synthesis, in S4 you program for a single key, in Storm you program for the whole stream. Storm gives you the basic tools to build a framework, while S4 gives you a well-defined framework. To use an analogy from Java build systems, Storm is more like Ant and S4 is more like Maven.

My personal preference here goes to S4, as it makes programming much easier. Most of the times in Storm you will anyway end mimicking the Actors model by implementing a hash based structure on a key, like in the example above.

### Data pipeline.

S4 uses a push model, events are pushed to the next PE as fast as possible. If receiver buffers get full events are dropped, and this can happen at any stage in the pipeline (from the Adapter to any PE).

Storm uses a pull model. Each bolt pulls event from its source, be it a spout or another bolt. Event loss can thus happen only at ingestion time, in the spouts if they cannot keep up with the external event rate.

In this case my preference goes to Storm, as it makes deployment much easier: you need to tune buffer sizes in order to deal peaks and event loss only at single place, the spout. If your deployment is badly sized in terms of parallelism level, at worst you get a performance hit in terms of throughput and latency, but the algorithm will produce the same result.

### Fault tolerance.

S4 provides state recovery via uncoordinated checkpointing. When a node crashes, a new node takes over its task and restarts from a recent snapshot of its state. Events sent after the last checkpoint and before the recovery are lost. Indeed, events can be lost in any case due to overload, so this design makes perfect sense. State recovery is very important for long running machine learning programs, where the state represents days or weeks worth of data.

Storm provides guaranteed delivery of events/tuples. Each tuple traverses the entire pipeline within a time interval or is declared as failed and can be replayed from the start by the spout. Spouts are responsible to keep tuples around for replay, or can rely on external services to do so (like Apache Kafka). However, the framework provides no state recovery.

I declare a tie here. State recovery is needed for many ML applications, although guaranteed delivery makes it easier to reason about the state of applications. Having both would be ideal, but implementing both of them without performance penalties is not trivial.

### Summary.

There are many other differences, but for sake of brevity I just present a short summary of the pros of each platform that the other one lacks.

#### S4 pros:

- Clean programming model.

- State recovery.

- Inter-app communication.

- Classpath isolation.

- Tools for packaging and deployment.

- Apache incubation.

#### Storm pros:

- Pull model.

- Guaranteed processing.

- More mature, more traction, larger community.

- High performance.

- Thread programming support.

- Advanced features (transactional topologies, Trident).

Now the hard question: *"Which one should I use for my new project?"*.

Unfortunately there is no easy answer, it mostly depends on your needs. I think the biggest factor to consider is whether you need guaranteed processing of events or state recovery. Also worth considering, Storm has a larger and more active user community, but the project is mainly a one-man effort, while S4 is in incubation with the ASF. This difference might be important if you are a large organization trying to decide on which platform to invest for the long term.
