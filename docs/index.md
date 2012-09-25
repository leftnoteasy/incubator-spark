---
layout: global
title: Spark Overview
---

{% comment %}
TODO(andyk): Rewrite to make the Java API a first class part of the story.
{% endcomment %}

Spark is a MapReduce-like cluster computing framework designed to support low-latency iterative jobs and interactive use from an interpreter. It exposes clean language-integrated APIs in [Scala](http://www.scala-lang.org) and Java, providing a wide array of parallel operations. Spark can run on top of the [Apache Mesos](http://incubator.apache.org/mesos/) cluster manager, Hadoop YARN, or without an independent resource manager ("standalone mode"). 

# Downloading

Get Spark by checking out the master branch of the Git repository, using `git clone git://github.com/mesos/spark.git`.

# Building

Spark requires [Scala 2.9.2](http://www.scala-lang.org/). You will need to have Scala's `bin` directory in your `PATH`,
or you will need to set the `SCALA_HOME` environment variable to point
to where you've installed Scala. Scala must be accessible through one
of these methods on slave nodes on your cluster.

Spark uses [Simple Build Tool](https://github.com/harrah/xsbt/wiki), which is bundled with it. To compile the code, go into the top-level Spark directory and run

    sbt/sbt package

# Testing the Build

Spark comes with a number of sample programs in the `examples` directory.
To run one of the samples, use `./run <class> <params>` in the top-level Spark directory
(the `run` script sets up the appropriate paths and launches that program).
For example, `./run spark.examples.SparkPi` will run a sample program that estimates Pi. Each of the
examples prints usage help if no params are given.

Note that all of the sample programs take a `<host>` parameter that is the Mesos master
to connect to. This can be a [Mesos master URL](http://www.github.com/mesos/mesos/wiki), or `local` to run locally with one
thread, or `local[N]` to run locally with N threads. You should start by using `local` for testing.

Finally, Spark can be used interactively from a modified version of the Scala interpreter that you can start through
`./spark-shell`. This is a great way to learn Spark.

# A Note About Hadoop Versions

Spark uses the Hadoop core library to talk to HDFS and other Hadoop-supported
storage systems. Because the HDFS protocol has changed in different versions of
Hadoop, you must build Spark against the same version that your cluster runs.
You can change the version by setting the `HADOOP_VERSION` variable at the top
of `project/SparkBuild.scala`, then rebuilding Spark (`sbt/sbt clean compile`).

# Where to Go from Here

Programming guides:
* [Spark Programming Guide]({{HOME_PATH}}scala-programming-guide.html): how to get started using Spark, and details on the Scala API
* [Java Programming Guide]({{HOME_PATH}}java-programming-guide.html): using Spark from Java

Deployment guides:
* [Running Spark on Amazon EC2]({{HOME_PATH}}ec2-scripts.html): scripts that let you launch a cluster on EC2 in about 5 minutes
* [Standalone Deploy Mode]({{HOME_PATH}}spark-standalone.html): launch a standalone cluster quickly without Mesos
* [Running Spark on Mesos]({{HOME_PATH}}running-on-mesos.html): deploy a private cluster using
    [Apache Mesos](http://incubator.apache.org/mesos)
* [Running Spark on YARN]({{HOME_PATH}}running-on-yarn.html): deploy Spark on top of Hadoop NextGen (YARN)

Miscellaneous:
* [Configuration]({{HOME_PATH}}configuration.html): customize Spark via its configuration system.
* [Bagel]({{HOME_PATH}}bagel-programming-guide.html): an implementation of Google's Pregel on Spark
* [Contributing to Spark](contributing-to-spark.html)

# Other Resources

* [Spark Homepage](http://www.spark-project.org)
* [AMP Camp](http://ampcamp.berkeley.edu/) - In 2012, the AMP Lab hosted the first AMP Camp which featured talks and hands-on exercises about Spark, Shark, Mesos, and more. [Videos, slides](http://ampcamp.berkeley.edu/agenda) and the [exercises](http://ampcamp.berkeley.edu/exercises) are all available online, and provide a great introduction to Spark.
* [Paper describing the programming model](http://www.cs.berkeley.edu/~matei/papers/2012/nsdi_spark.pdf)
* [Code Examples](http://spark-project.org/examples.html): more are also available in the [examples subfolder](https://github.com/mesos/spark/tree/master/examples/src/main/scala/spark/examples) of Spark
* [Mailing List](http://groups.google.com/group/spark-users): ask here for help

# Community

To keep up with Spark development or get help, sign up for the [spark-users mailing list](http://groups.google.com/group/spark-users).

If you're in the San Francisco Bay Area, there's a regular [Spark meetup](http://www.meetup.com/spark-users/) every few weeks. Come by to meet the developers and other users.

If you'd like to contribute code to Spark, read [how to contribute]({{HOME_PATH}}contributing-to-spark.html).