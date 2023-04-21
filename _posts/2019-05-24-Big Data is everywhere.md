. The first major project involving data dates back to 1937, when the government needed to keep track of social security contributions of 26 million people and 3 million companies as per the Social Security Act. The government gave the contract to IBM to develop punch card-reading machine for the bookkeeping. Fast forward to 21st century where the data requirements have grown exponentially.
In 2010, Eric Schmidt quoted Techonomy conference that "there were 5 exabytes of information created by the entire world between the dawn of civilization and 2003. Now that same amount is created every two days."

Google has been on the forefront to meet the big data challenge headlong. One of Google’s first challenges was to figure out how to index the exploding volume of content on the web. To solve this, Google invented a new style of data processing known as MapReduce to manage large-scale data processing across large clusters of commodity servers. MapReduce is a programming model and an associated implementation for processing and generating large data sets. They published the map reduce framework paper in 2004. That became the inspiration behind Hadoop.


All the google products rely on data, so they designed a distributed storage system called bigtable. They published the big table paper in 2006. At that time bigtable was used by more than sixty Google products and projects, including Google Analytics, Google Finance, Orkut, Personalized Search, Writely, and Google Earth. Some of these products and projects are no longer with us but the legacy of bigtable lives with us through HBase. BigTable used the infrastructure of Google File System that was the inspiration for HDFS.

A Bigtable is a sparse, distributed, persistent multidimensional sorted map. The map is indexed by a row key, column key, and a timestamp; each value in the map is an uninterpreted array of bytes. (row:string, column:string, time:int64) → string. Bigtable stores the data in lexicographical order as row keys. This helps to keep related data together. For instance they use reverse URL (com.google) as a key. This helps them search and report data and analytics on related websites faster. Bigtable also has the concept of column families that allows related columns to be compressed.

With Google’s multiple online services splitting tasks into tiny pieces and spreading them across a vast network of machines, Google needed a way of controlling access to those machines. So they developed Chubby, a distributed lock service intended for coarse-grained synchronization of activities within Google’s distributed systems. The primary goals included reliability, availability to a moderately large set of clients, and easy-to-understand semantics.
The Chubby lock service paper published in 2006 formed the basis for development of Zookeeper that is used extensively with HBASE.

In summary, the business paradigm of Google is based on large amounts of data. Instead of trying the time-tested ways of adding expensive hardware, the Google Engineers thought outside the box. They came up with innovative solutions that used commodity software and could scale horizontally. There were many naysayers at the time but the past decade has proven them right. Thinking outside the box and finding new ways to look at a problem is the key to creativity and innovation.



[https://datafloq.com/read/big-data-history/239](https://datafloq.com/read/big-data-history/239)
[https://mapr.com/blog/5-google-projects-changed-big-data-forever/](https://mapr.com/blog/5-google-projects-changed-big-data-forever/)
[http://static.googleusercontent.com/media/research.google.com/en/us/archive/mapreduce-osdi04.pdf](http://static.googleusercontent.com/media/research.google.com/en/us/archive/mapreduce-osdi04.pdf)
[https://static.googleusercontent.com/media/research.google.com/en//archive/bigtable-osdi06.pdf](https://static.googleusercontent.com/media/research.google.com/en//archive/bigtable-osdi06.pdf)
