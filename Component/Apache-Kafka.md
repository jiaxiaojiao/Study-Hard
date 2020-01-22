## Apache Kafka

> A distributed streaming platform.

### 目录
* [Kafka是什么？](#Kafka是什么？)
* [什么是分布式流平台？](#什么是分布式流平台？)
* [参考](#参考)

### Kafka是什么？

Kafka是由Apache软件基金会开发的一个开源流处理平台，由Scala和Java编写。Kafka是一种高吞吐量的分布式发布订阅消息系统

### 什么是分布式流平台？

Apache Kafka® is a distributed streaming platform. What exactly does that mean?

A streaming platform has three key capabilities:
* Publish and subscribe to streams of records, similar to a message queue or enterprise messaging system.
* Store streams of records in a fault-tolerant durable way.
* Process streams of records as they occur.

Kafka is generally used for two broad classes of applications:
* Building real-time streaming data pipelines that reliably get data between systems or applications
* Building real-time streaming applications that transform or react to the streams of data

To understand how Kafka does these things, let's dive in and explore Kafka's capabilities from the bottom up.

First a few concepts:
* Kafka is run as a cluster on one or more servers that can span multiple datacenters.
* The Kafka cluster stores streams of records in categories called topics.
* Each record consists of a key, a value, and a timestamp.

Kafka has four core APIs:
* The Producer API allows an application to publish a stream of records to one or more Kafka topics.
* The Consumer API allows an application to subscribe to one or more topics and process the stream of records produced to them.
* The Streams API allows an application to act as a stream processor, consuming an input stream from one or more topics and producing an output stream to one or more output topics, effectively transforming the input streams to output streams.
* The Connector API allows building and running reusable producers or consumers that connect Kafka topics to existing applications or data systems. For example, a connector to a relational database might capture every change to a table.

In Kafka the communication between the clients and the servers is done with a simple, high-performance, language agnostic TCP protocol. This protocol is versioned and maintains backwards compatibility with older version. We provide a Java client for Kafka, but clients are available in many languages.

### 已发布版本

* 2.3.1    Released Oct 24, 2019
* 2.3.0    Released Jun 25, 2019
* 2.2.0    Released Mar 22, 2019
* 2.1.0    Released Nov 20, 2018
* 2.0.0    Released July 30, 2018
* 1.1.0    Released March 28, 2018
* 1.0.0    Released November 1, 2017
* 0.7.0    Released January 4, 2012

### 参考
* 网站： http://kafka.apache.org/
* 百度百科