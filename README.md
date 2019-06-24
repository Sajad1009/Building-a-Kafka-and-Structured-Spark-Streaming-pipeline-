Large number of companies across a multitude of industries are currently maintaining data pipelines used to ingest and analyze
a huge data streams. In effect, the proper implementation of such pipelines belongs to the realm of “data engineering”,
and represents a gateway to interesting data science-related problems. Traditional machine learning methods have been developed to work
using batch or offline approaches,but there are fewer options when we start considering solutions for true streaming problems.

Spark Streaming is an extension of the core Spark API that enables scalable, high-throughput, fault-tolerant stream processing of live
data streams. Data can be ingested from many sources like Kafka, Flume, Kinesis, or TCP sockets, and can be processed using complex
algorithms expressed with high-level functions like map, reduce, join and window. Finally, processed data can be pushed out to filesystems, databases, and live dashboards.
In fact, you can apply Spark’s machine learning and graph processing algorithms on data streams.

![](streaming-arch.png)

Internally, it works as follows. Spark Streaming receives live input data streams and divides the data into batches, which are then processed by the Spark engine to generate the final stream of results in batches.

![](streaming-flow.png)


Spark Streaming provides a high-level abstraction called discretized stream or DStream, which represents a continuous stream of data. DStreams can be created either from input data streams from sources such as Kafka, Flume, and Kinesis, or by applying high-level operations on other DStreams. Internally, a DStream is represented as a sequence of RDDs.

This guide shows you how to start writing Spark Streaming programs with DStreams. You can write Spark Streaming programs in Scala, Java or Python (introduced in Spark 1.2), all of which are presented in this guide. You will find tabs throughout this guide that let you choose between code snippets of different languages.

Note: There are a few APIs that are either different or not available in Python. Throughout this guide, you will find the tag Python API highlighting these differences.

![](kafka_spark_pipeline.png)


Lets strat with coding side:------


### setting up your  java environnment in your system 

I am not going to cover that here.... However I provided some link below to take you through the process 

https://confluence.atlassian.com/doc/setting-the-java_home-variable-in-windows-8895.html

### Zookeeper Installing Zookeeper

```
sak@sajad-m:~$ wget http://apache.stu.edu.tw/zookeeper/zookeeper-3.5.5/apache-zookeeper-3.5.5-bin.tar.gz

sak@sajad-m:~$ tar -zxf apache-zookeeper-3.5.5-bin.tar.gz

sak@sajad-m:~$ cd apache-zookeeper-3.5.5-bin

## At this point, you can create a new directory data using the mkdir command

sak@sajad-m:~/apache-zookeeper-3.5.5-bin$ mkdir data

and also edit the Zookeeper configuration file located in the conf directory with the command

vim conf/zoo.cfg  

--------------------------

tickTime=2000
dataDir=/path_to_your_working_directory/zookeeper-3.5.5-bin/data
clientPort=2181
initLimit=5
syncLimit=2

--------------------------
```
### Starting Zookeeper

```
sak@sajad-m:~/apache-zookeeper-3.5.5-bin$ zkServer.sh start

output 


ZooKeeper JMX enabled by default
Using config: /home/sak/apache-zookeeper-3.5.5-bin/bin/../conf/zoo.cfg
Starting zookeeper ... STARTED

```

You can also launch the Zookeeper CLI, which will allow you to connect to the Zookeeper server:

```
with command sak@sajad-m:~/apache-zookeeper-3.5.5-bin$ zkCli.sh

```

## Apache Kafka

apache Kafka is an open-source stream-processing software platform developed by LinkedIn and donated to the Apache Software Foundation, written in Scala and Java. The project aims to provide a unified, high-throughput, low-latency platform for handling real-time data feeds.

Lets donwnload apache kafka with the code below 

```
wget https://www-us.apache.org/dist/kafka/2.2.1/kafka_2.11-2.2.1.tgz

tar -zxf kafka_2.11-2.2.1.tgz 

cd kafka_2.11-2.2.1  

```
### Starting the Kafka server


Because Kafka depends on Zookeeper to maintain and distribute tasks, we need to start ZooKeeper before starting the Kafka broker.

```
zookeeper-server-start.sh config/zookeeper.properties

kafka-server-start.sh config/server.properties

```

Now you can strat a new topic

```

kafka-topics.sh --create --zookeeper localhost:2181 --replication-factor 1 --partitions 1 --topic test-topic  ## name you topic 

```

We can also list the topics currently in the Kafka server by using the kafka-topics.sh utility script

```
kafka-topics.sh --list --zookeeper localhost:2181

```

##Producing and consuming messages with Kafka

first we have to start producer to start sending messages  with the command below 

```
sak@sajad-m:~/kafka_2.11-2.2.0$ kafka-console-producer.sh --brokeist localhost:9092 --topic test-topic

and send message 
-----------------------------
Hello it me 

We learning new things 
-------------------------------
```

 #### Now we should get spark ready in our system  I am not going to cover how to install spark in the system howover google cloud  clusters and many platforms come with pre-installed apache spark 
 
 
 
















