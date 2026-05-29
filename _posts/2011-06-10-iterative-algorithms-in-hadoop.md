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
category_names:
  - "PhD"
tag_names:
  - "algorithm"
  - "hadoop"
  - "iterative"
  - "mapreduce"
comments: false
sitemap: false
wp_id: 228
wp_slug: "iterative-algorithms-in-hadoop"
permalink_slug: "iterative-algorithms-in-hadoop"
wp_url: "https://gdfm.me/2011/06/10/iterative-algorithms-in-hadoop/"
---

While speaking about [my latest work](/blog/2011/03/social-content-matching-in-mapreduce-vldb/ "Social Content Matching in MapReduce") with some researchers, they confessed me they were very curious about how to implement an iterative algorithm in MapReduce/Hadoop. They made me realize that the task is not exactly straightforward, so I decided to write a post about it, and here we are.
The general idea for iterative algorithms in MapReduce is to chain multiple jobs together, using the output of the last one as the input of the next one. An important consideration is that, given the usual size of the data, the termination condition must be computed within the MapReduce program. The standard MapReduce model does not offer simple elegant ways to do this, but Hadoop has some added features that simplify this task: [Counters](http://philippeadjiman.com/blog/2010/01/07/hadoop-tutorial-series-issue-3-counters-in-action/ "A simple tutorial on counters").
To check for a termination condition with Hadoop counters, you run the job and collect statistics while its running. Then you access the counters and get their values, you might also compute derivate measures from counters and finally decide whether to continue iterating or to stop.
Here an example. The code is only partial, it's intended just to show the technique. Suppose we want to do some directed graph processing using a diffusion process (the exact application doesn't matter, I am using a coloring example here). Assume the mapper propagates the information along the graph and the reducer computes the new one.
<pre>    public static enum Color {
        RED, GREEN, BLUE;
    }

    public static enum State {
        UPDATED;
    }

    public static class ExampleReducer extends Reducer&lt;Vertex, Edge, Vertex, Edge&gt; {

        @Override
        protected void reduce(Vertex key, Iterable&lt;Edge&gt; inLinks, Context context) {
            int numRed=0, numGreen=0, numBlue=0;
            for (Edge e : inLinks) {
                switch (e.color()) {
                case RED:
                    numRed++;
                    break;
                case GREEN:
                    numGreen++;
                    break;
                case BLUE:
                    numBlue++;
                    break;
                default:
                    assert false : "Unexpected color " + e;
                }
            }
            context.getCounter(RED).increment(numRed);
            context.getCounter(GREEN).increment(numGreen);
            context.getCounter(BLUE).increment(numBlue);

            Color currentColor = key.color();
            Color newColor = computeNewColor(numRed, numGreen, numBlue);
            if (currentColor != newColor) {
                context.getCounter(UPDATED).increment(1);
                key.setColor(newColor);
            }
            for (Edge e : key.outLinks()) {
                e.setColor(newColor);
                context.write(key, e);
            }
        }</pre>
In this snippet, we scan the incoming edges for each vertex and compute the number of edges for each color. Then we proceed to compute the new color based on some procedure (omitted for brevity) and write the updated results.
After the scan, we use the counters to report how many edges of each color we have seen. At the end of the job we will have a global view of the colors in the graph.
If we update the vertex with a new color, we report it using another counter (UPDATED). At the end of the job this counter will tell us how many updates have been performed during this round.
Now suppose we want to run this algorithm up to stabilization, that is up to the point where no more updates will occur. To do this, we can simply check the number of updates reported by the counter and stop when it reaches zero. This must be done in the driver program, in between successive invocations of the MapReduce job.
Another important thing for an iterative algorithm in Hadoop is defining a naming schema for the iterations. The simplest thing is to create a working directory based on the input or output name. Every iteration will use a directory inside the working directory for input and output.
<pre>    @Override
    public int run(String[] args) throws Exception {
        int iteration = 0, result = 0;
        boolean verbose = false;
        Path inputPath = new Path(args[0]);
        Path basePath = new Path(args[1] + "_iterations");
        FileSystem fs = FileSystem.get(getConf());
        assert fs.exists(inputPath) : "Input path does not exist: " + inputPath;
        // working directory
        fs.delete(basePath, true);
        fs.mkdirs(basePath);

        // copy input into working dir
        Path outputPath = new Path(basePath, iteration + "");
        Job job0 = getPrototypeJob(iteration);
        FileInputFormat.setInputPaths(job0, inputPath);
        FileOutputFormat.setOutputPath(job0, outputPath);
        job0.setMapperClass(InitMapper.class);
        job0.setReducerClass(InitReducer.class);
        if (! job0.waitForCompletion(verbose) )
            return -1;

        boolean hasUpdates = true;
        while (hasUpdates) {
            iteration++; // iteration counter
            inputPath = outputPath; // new input is the old output
            outputPath = new Path(basePath, iteration + "");
            Job job = getPrototypeJob(iteration);
            FileInputFormat.setInputPaths(job, inputPath);
            FileOutputFormat.setOutputPath(job, outputPath);
            job.setMapperClass(ExampleMapper.class);
            job.setReducerClass(ExampleReducer.class);
            if (! job.waitForCompletion(verbose) );
                return -1;
            // remove temporary files as you go, this is optional
            fs.delete(inputPath, true);
            // retrieve the counters
            long redEdges = job.getCounters().findCounter(RED).getValue();
            long greenEdges = job.getCounters().findCounter(GREEN).getValue();
            long blueEdges = job.getCounters().findCounter(BLUE).getValue();
            System.out.println(String.format(
                "red %d, green%d, blue %d", redEdges, greenEdges, blueEdges));
            long updates = job.getCounters().findCounter(UPDATED).getValue();
            // compute termination condition
            hasUpdates = (updates &gt; 0);
        }
        return 0;
    }

    private Job getPrototypeJob(int iteration) throws IOException {
        Job job = new Job(getConf(), "Iteration " + iteration);
        job.setInputFormatClass(SequenceFileInputFormat.class);
        job.setOutputFormatClass(SequenceFileOutputFormat.class);
        job.setMapOutputKeyClass(Vertex.class);
        job.setMapOutputValueClass(Edge.class);
        job.setOutputKeyClass(Vertex.class);
        job.setOutputValueClass(Edge.class);
        return job;
    }</pre>
This snippet shows the driver program, usually realized by implementing the org.apache.hadoop.util.Tool interface and overriding the run() method. In the first part the driver interacts with the file system to create the working directory. Then we launch our first job which serves a double purpose, it copies the input in the working directory and performs any initial preprocessing needed. Finally, in the third part we start our iterations.
For each job, the input is the output of the last run. The output goes into the working directory with an increasing counter added at the end. After the job finishes we remove the temporary files (this is useful if we perform many iterations with many reducers and we have quotas on the namenode). We also access the counters to print a summary view of the graph and to compute the termination condition.
That's it. Not too complicated after all :)
