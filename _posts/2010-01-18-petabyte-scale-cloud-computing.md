---
layout: "post"
title: "Petabyte scale Cloud Computing"
date: "2010-01-18 22:00:21"
last_modified_at: "2010-01-18 22:00:21"
author: "melmeric"
permalink: "/blog/2010/01/petabyte-scale-cloud-computing/"
categories:
  - "phd"
tags:
  - "cloud"
  - "cnr"
  - "mapreduce"
  - "pdbms"
  - "seminar"
category_names:
  - "PhD"
tag_names:
  - "cloud"
  - "cnr"
  - "mapreduce"
  - "pdbms"
  - "seminar"
comments: false
sitemap: false
wp_id: 26
wp_slug: "petabyte-scale-cloud-computing"
permalink_slug: "petabyte-scale-cloud-computing"
wp_url: "https://gdfm.me/2010/01/18/petabyte-scale-cloud-computing/"
---

Today I presented my PhD research topic at [ISTI CNR](http://www.isti.cnr.it/ "ISTI CNR"), institute of computer science and technology from the Italian National Research Council.
I have been working with the [HPC lab](http://hpc.isti.cnr.it/ "HPC Lab") since late November 2009, when I chose my thesis supervisor, [Claudio Lucchese](http://hpc.isti.cnr.it/~claudio/ "Claudio Lucchese").
The topic of the [seminar](http://hpc.isti.cnr.it/?p=236) was **"How to survive the Data Deluge: Petabyte scale Cloud Computing"**.
In the seminar I gave an introduction to the problem of large scale data management and to its motivations. I described the new technologies that are used today to perform analysis on these large datasets (mainly focusing on the **MapReduce** paradigm) and the difference with the other competing technology, **Parallel DBMS**.
There is a very harsh ongoing debate on which technology is the best one, as there are advantages on both sides. One of the main detractors of the MapReduce paradigm is [Michael Stonebraker](http://en.wikipedia.org/wiki/Michael_Stonebraker), Professor of Computer Science at MIT and strong DataBase supporter, given also that he co-founded one of the companies that produces [Vertica](http://www.vertica.com/), a PDBMS that targets more or less the same analytical workloads of MapReduce, even if in a different fashion.
He published a [post](http://databasecolumn.vertica.com/database-innovation/mapreduce-a-major-step-backwards), together with Prof. DeWitt, in which he basically blamed MapReduce for not being a DataBase. The post received very [harsh](http://scienceblogs.com/goodmath/2008/01/databases_are_hammers_mapreduc) [critiques](http://glinden.blogspot.com/2008/01/mapreduce-step-backwards.html) (read also the comments to the original post as they are very interesting). Stonebraker and DeWitt doubled with another [post](http://databasecolumn.vertica.com/database-innovation/mapreduce-ii) in which they replied to the answers they received, providing examples of DataBase superiority. They then decided to push this forward and published a [paper](http://database.cs.brown.edu/projects/mapreduce-vs-dbms/) comparing the two systems on various workloads, showing how Vertica is far superior to Hadoop in almost all tasks.
The last page in this story is in [this month's Communications of the ACM](http://cacm.acm.org/magazines/2010/1). I said page but they are actually pages, because the editor published two very interesting articles [side](http://cacm.acm.org/magazines/2010/1/55743-mapreduce-and-parallel-dbmss-friends-or-foes) by [side](http://cacm.acm.org/magazines/2010/1/55744-mapreduce-a-flexible-data-processing-tool). The first one is the latest from the Stonebraker&DeWitt couple, that basically says MapReduce and PDBMS serve different purposes and have to coexist. The latest one is a reply by the original authors of MapReduce (Jeffrey Dean and **Sanjay Ghemawat) to all the critiques to their creature. They show how most of the flaws identified by S&DW are actually implementation problems rather than limits of the paradigm. Dean and Ghemawat also let slip through that the comparison performed in their article is biased towards database oriented tasks. In their words *"The conclusions about performance in the comparison paper were based on flawed assumptions about MapReduce and overstated the benefit of parallel database systems"***
**I will abstain from commenting on this issue for now, even though I deem it as very interesting for my future research. I just think I do not have matured my opinion enough to express it.**
**In the meanwhile, here is the slide deck I used for my presentation.**
**[Petabyte Scale Cloud Computing](/assets/media/2010/01/petabyte-scale-cloud-computing.pdf)**
