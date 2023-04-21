The last two weeks were dedicated to distributed computing and distributed storage. Map reduce paradigm revolutionized computing as it brought compute near the storage. In the map reduce framework, each step reads data from disk, does a map or reduce operation. In 2009 Matei Zahara developed Saprk as part of his PHD thesis at University of Berkeley Amplab. 
As per the white paper on RDD
“Most current cluster computing systems are based on an acyclic data flow model, where records are loaded from stable storage (e.g., a distributed file system), passed through a DAG of deterministic operators, and written back out to stable storage. While acyclic data flow is a powerful abstraction, there are applications that cannot be expressed efficiently using only this construct. Our work focuses on one broad class of applications not well served by the acyclic model: those that reuse a working set of data in multiple parallel operations. This class includes iterative algorithms commonly used in machine learning and graph applications, which apply a similar function to the data on each step, and interactive data mining tools, where a user repeatedly queries a subset of the data. Because dataflow based frameworks do not explicitly provide support for working sets, these applications have to output data to disk and reload it on each query with current systems ,leading to significant overhead.”

Spark execution engine that Matei Zahara created is very versatile. It can run on local file system or HDFS. It can run stand alone or on cluster. It can run in batch mode as well as streaming. It is gaining popularity for machine learning as well.

When I had started learning spark last year, the terminology confused me.  There are master/slaves(workers), driver/executors. People say forget about master/slaves(workers) but somehow all the websites and blogs talk about them. 
Hence, I decided to delve into the roles of driver/executor a little more for the blog. 
Master and Slave come into picture only when we run in cluster configuration and not we run spark on local machine or stand-alone mode. Essentially this is just the hardware management aspect.

A user interaction with Spark comes via Driver and Executor.  Developers write a driver program that connects to clusters to run workers. The spark driver’s location is independent of the master/slaves. It could co-locate with the master or run it from another node. The only requirement is that it must be in a network addressable from the Spark Workers. 

A Spark driver is the process that creates and owns an instance of SparkContext. The spark context contains the information about the environment.  The driver takes the user’s application (also called driver program) and creates RDDs and DAG scheduler. It splits a Spark application into tasks and schedules them to run on executors. A driver is where the task scheduler lives and spawns tasks across workers. A driver coordinates workers and overall execution of tasks.

When we run the spark shell or jupyter notebook and execute commands, the driver does not know about the application program in advance. In this scenario the spark interpreter takes the command and creates a scala class. The class is serialized and sent to the executors for executing the commands.

After all this research I have a new respect for the Spark Driver and looking forward to learning more about it.   



•	The driver prepares the context and declares the operations on the data using RDD transformations and actions.
•	The driver submits the serialized RDD graph to the master. The master creates tasks out of it and submits them to the workers for execution. It coordinates the different job stages.
•	The workers is where the tasks are actually executed. They should have the resources and network connectivity required to execute the operations requested on the RDDs.

When you submit a Spark job, the driver implicitly converts the code containing transformations and actions performed on the RDDs into a logical Directed Acyclic Graph (DAG). The driver program also performs certain optimizations like pipelining transformations and then it converts the logical DAG into physical execution plan with set of stages. A Stage is a combination of transformations which does not cause any shuffling, pipelining as many narrow transformations (eg: map, filter etc) as possible.

repartition() shuffles the data between the executors and divides the data into number of partitions. But this might be an expensive operation since it shuffles the data between executors and involves network traffic. Ideal place to partition is at the data source, while fetching the data. Things can speed up greatly when data is partitioned the right way but can dramatically slow down when done wrong, especially due the Shuffle operation.

Shuffle Operation or wide transformation define the boundary of 2 stages.Stages are separated by 2 shuffle operations.


For example, an RDD representing an HDFS file has a partition for each block of the file and knows which nodes each block is on from HDFS. Meanwhile, the result of a map on this RDD has the same partitions, but applies the map function to the parent’s data when computing its elements. 
We found it both sufficient and useful to classify dependencies into two types: narrow dependencies, where each partition of the child RDD depends on a constant number of partitions of the parent (not proportional to its size), and wide dependencies, where each partition of the child can depend on data from all partitions of the parent. For example, map leads to a narrow dependency, while join leads to to wide dependencies (unless the parents are hash-partitioned). 


Overall, our scheduler is similar to Dryad’s [18], but additionally takes into account which partitions of RDDs are available in caches. The scheduler examines the lineage graph of the target RDD to builds a DAG of stages to execute. Each stage contains as many pipelined transformations with narrow dependencies as possible. The boundaries of the stages are the shuffle operations required for wide dependencies, or any cached partitions that can short-circuit the computation of a parent RDD. Figure 6 shows an example. We launch tasks to compute missing partitions from each stage when its parents end. The scheduler places tasks based on data locality to minimize communication. If a task needs to process a cached partition, we send it to a node that has that partition. Otherwise, if a task processes a partition for which the containing RDD provides preferred locations (e.g., due to data locality in HDFS), we send it to those. For wide dependencies (i.e., shuffle dependencies), we currently materialize intermediate records on the nodes holding parent partitions to simplify fault recovery, much like MapReduce materializes map outputs

We evaluated Spark and RDDs through a series of experiments on Amazon EC2 [1], including comparisons with Hadoop and benchmarks of user applications. Overall, our results show the following: • Spark outperforms Hadoop by up to 20× in iterative machine learning applications. The speedup comes from storing data in memory and from avoiding deserialization cost by caching Java objects.
We evaluated Spark and RDDs through a series of experiments on Amazon EC2 [1], including comparisons with Hadoop and benchmarks of user applications. Overall, our results show the following: • Spark outperforms Hadoop by up to 20× in iterative machine learning applications. The speedup comes from storing data in memory and from avoiding deserialization cost by caching Java objects.


[https://spark.apache.org/research.html](https://spark.apache.org/research.html)
[https://www2.eecs.berkeley.edu/Pubs/TechRpts/2011/EECS-2011-82.pdf](https://www2.eecs.berkeley.edu/Pubs/TechRpts/2011/EECS-2011-82.pdf)
[https://www.xplenty.com/blog/apache-spark-vs-hadoop-mapreduce/](https://www.xplenty.com/blog/apache-spark-vs-hadoop-mapreduce/)
[https://medium.com/@thejasbabu/spark-under-the-hood-partition-d386aaaa26b7](https://medium.com/@thejasbabu/spark-under-the-hood-partition-d386aaaa26b7)
[https://medium.com/parrot-prediction/partitioning-in-apache-spark-8134ad840b0](https://medium.com/parrot-prediction/partitioning-in-apache-spark-8134ad840b0)
[https://medium.com/@goyalsaurabh66/spark-basics-rdds-stages-tasks-and-dag-8da0f52f0454](https://medium.com/@goyalsaurabh66/spark-basics-rdds-stages-tasks-and-dag-8da0f52f0454)
[https://stackoverflow.com/questions/24637312/spark-driver-in-apache-spark](https://stackoverflow.com/questions/24637312/spark-driver-in-apache-spark)
[https://medium.com/@ostechtalks/apache-spark-internals-part-1-dont-get-carried-away-with-ease-of-use-aceacca63ed9](https://medium.com/@ostechtalks/apache-spark-internals-part-1-dont-get-carried-away-with-ease-of-use-aceacca63ed9)

