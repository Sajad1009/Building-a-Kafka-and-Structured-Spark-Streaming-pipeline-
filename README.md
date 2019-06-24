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

![]kafka_spark_pipeline.png
