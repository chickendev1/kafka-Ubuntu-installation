# kafka-installation

This is the step by step tutorial to install Kafka, Kafka tool, produce and consume topic on ubuntu 16.04

## Here’s some very basic concepts you need to understand:

A stream of messages of a particular type is defined as a topic. A message is defined as a payload of bytes and a Topic is a category or feed name to which messages are published.
A Producer can be anyone who can publish messages to a Topic.
The published messages are then stored at a set of servers called Brokers or Kafka Cluster.
A Consumer can subscribe to one or more Topics and consume the published Messages by pulling data from the Brokers.
Zookeeper: As for coordination and facilitation of distributed system ZooKeeper is used, for the same reason Kafka is using it. ZooKeeper is used for managing, coordinating Kafka broker.

Kafka consists of Records, Topics, Consumers, Producers, Brokers, Logs, Partitions, and Clusters. Records can have key (optional), value and timestamp. Kafka Records are immutable. A Kafka Topic is a stream of records ("/orders", "/user-signups"). You can think of a Topic as a feed name. A topic has a Log which is the topic’s storage on disk. A Topic Log is broken up into partitions and segments. The Kafka Producer API is used to produce streams of data records. The Kafka Consumer API is used to consume a stream of records from Kafka. A Broker is a Kafka server that runs in a Kafka Cluster. Kafka Brokers form a cluster. The Kafka Cluster consists of many Kafka Brokers on many servers. Broker sometimes refer to more of a logical system or as Kafka as a whole.

Kafka topic is a named stream of records. Kafka stores topics in logs. A topic log is broken up into partitions. Kafka spreads log’s partitions across multiple servers or disks. Think of a topic as a category, stream name or feed.
Topics are inherently published and subscribe style messaging. A Topic can have zero or many subscribers called consumer groups. Topics are broken up into partitions for speed, scalability, and size.

http://cloudurable.com/blog/kafka-architecture/index.html

## How to install?

Step1: update and install Java. This tutorial is on JDK 1.8

```
java -version
java version "1.8.0_161"
Java(TM) SE Runtime Environment (build 1.8.0_161-b12)
Java HotSpot(TM) 64-Bit Server VM (build 25.161-b12, mixed mode)
```
Step2: download Kafka : http://kafka.apache.org/downloads.html

```
tar -zxvf  kafka_2.11-1.1.0.tgz -C /opt/kafka
```

Step3: cd to kafka directory and start Zookeeper

```
bin/zookeeper-server-start.sh config/zookeeper.properties
```
By default, Zookeper will listen on port 2181.

Step4: start kafka brokers
```
bin/kafka-server-start.sh config/server.properties
```

[!!] turn on topic delete
  ```
  sudo nano /config/server.properites
  ```
  #>> At end of file add:
  ```
  delete.topic.enable = true
  ```
  #>> save and quit

Step5: create topic named topic-test
```
/bin/kafka-topics.sh --create --topic topic-test --zookeeper localhost:2181 --partitions 1 --replication-factor 1
```
Step6: send message as producer 
```
echo "hello world" | bin/kafka-console-producer.sh --broker-list localhost:9092 --topic topic-test
```
Step7: run consummer
```
bin/kafka-console-consumer.sh --zookeeper localhost:2181 --topic topic-test --from-beginning
```

Step8: download Kafka tools from http://www.kafkatool.com/download.html
Run the sh file to install
Config and connect to Zookeeper default port: 2181

Example: Sample project using Kafka
https://github.com/chickendev1/kafka-sample-project
