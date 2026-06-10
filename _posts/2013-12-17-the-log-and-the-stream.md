---
layout: "post"
title: "The log and the stream"
date: "2013-12-17 13:03:24"
last_modified_at: "2013-12-17 13:03:24"
author: "melmeric"
permalink: "/blog/2013/12/the-log-and-the-stream/"
categories:
  - "technology"
tags:
  - "linkedin"
  - "log"
  - "stream-processing"
comments: false
---

> LinkedIn, for example, has almost **no batch data collection at all**. The majority of our data is either activity data or database changes, both of which occur continuously. In fact, **when you think about any business, the underlying mechanics are almost always a continuous process**—events happen in real-time, as Jack Bauer would tell us. When data is collected in batches, it is almost always due to some manual step or lack of digitization or is a historical relic left over from the automation of some non-digital process. Transmitting and reacting to data used to be very slow when the mechanics were mail and humans did the processing. A first pass at automation always retains the form of the original process, so this often lingers for a long time.
>
> Production "batch" processing jobs that run daily are often effectively mimicking a kind of continuous computation with a window size of one day. The underlying data is, of course, always changing. These were actually so common at LinkedIn (and the mechanics of making them work in Hadoop so tricky) that we implemented a whole framework for managing incremental Hadoop workflows.
>
> Seen in this light, it is easy to have a different view of stream processing: it is just processing which includes a notion of time in the underlying data being processed and does not require a static snapshot of the data so it can produce output at a user-controlled frequency instead of waiting for the "end" of the data set to be reached. In this sense, **stream processing is a generalization of batch processing**, and, given the prevalence of real-time data, a very important generalization.
>
>

(emphasis added by me)

via [The Log: What every software engineer should know about real-time data's unifying abstraction \| LinkedIn Engineering](http://engineering.linkedin.com/distributed-systems/log-what-every-software-engineer-should-know-about-real-time-datas-unifying).
