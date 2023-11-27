# Learning Apache Kafka

## Introduction
This article will help readers understand what Kafka is, why it is used, and how it works. **Apache Kafka**, an open-source stream-processing software platform developed by the Apache Software Foundation, written in Scala and Java. Designed with the fundamental premise of enabling high-throughput, fault-tolerant, publish-subscribe messaging systems, Kafka has become an essential tool in the handling of real-time data feeds.

### Main Concepts and Terminology

![image](https://mindmajix.com/_next/image?url=https%3A%2F%2Fcdn.mindmajix.com%2Fblog%2Fimages%2Fkafka-ecosystem-250120.png&w=1200&q=75)

The above diagram shows the Kafka cluster architecture. The elements of the Kafka cluster architecture can be explained in the following way:

- **Brokers**: Kafka clusters consist of one or more servers, each of which is called a broker. Usually Kafka cluster contains several brokers to preserve load balance. As Kafka clusters do not have states, they take zookeeper’s help to sustain cluster state.
- **ZooKeeper**: The primary responsibility of Zookeeper is to manage and synchronize the Kafka broker. The zookeeper will notify the producer and consumer regarding the existence of the new broker or the breakdown of the broker. According to this notification, the producer and consumer will take the decision and starts synchronizing their activities with another broker.
- **Producer**: The primary role of a Kafka producer is to publish (push) messages to Kafka topics. The topics are managed by brokers within the Kafka cluster.
- **Consumer**: The primary role of a Kafka consumer is to read messages from the Kafka topics. As the brokers do not keep track of which messages have been consumed, it's the responsibility of the consumers to keep tabs on their progress through the message stream.

![image](https://cdn.thenewstack.io/media/2017/02/5648a9e9-kafka-arch.png)

The above diagram illustrates the basic components and their interactions within a Kafka system:

- **Producers**: Entities that publish (push) data to topics. In the diagram, Producer A and Producer B are shown sending messages to a Kafka topic.
- **Topics**: A category or feed name to which messages are published. Very simplified, a topic is similar to a folder in a filesystem, and the data are the files in that folder. Topics in Kafka are multi-subscriber; that is, a topic can have zero, one, or many consumers that subscribe to the data written to it. "My Topic" is the Kafka topic in this case.
- **Partition**: Topics are split into partitions (Partition 1, Partition 2, Partition 3), which allow for parallelism in both writing and reading data. Each partition is an ordered, immutable sequence of records.
- **Consumers**: Entities that subscribe to topics and process the published messages. Consumer A, B, and C are shown each consuming from a specific partition.


## Why Kafka
Apache Kafka is a powerful tool in data processing and streaming, favored for its ability to handle high volumes of data with high throughput and low latency. Its distributed architecture ensures scalability and fault tolerance, making it reliable for critical applications. Kafka facilitates real-time data processing with its stream processing capabilities and is versatile in handling various data formats. Additionally, its integration with a wide range of systems and strong community support make it a go-to choice for complex data architectures in various applications.

## Quick Start
### Step 1: Download Kafka
[Download](https://www.apache.org/dyn/closer.cgi?path=/kafka/3.6.0/kafka_2.13-3.6.0.tgz) the latest Kafka release and extract it:

```bash
$ tar -xzf kafka_2.13-3.6.0.tgz
$ cd kafka_2.13-3.6.0
```

### Step 2: Set Up the Environment
***NOTE: Your local environment must have Java 8+ installed.***

Run the following commands in order to start all services in the correct order:

```bash
# Start the ZooKeeper service
$ bin/zookeeper-server-start.sh config/zookeeper.properties
```

Open *another* terminal session and run:
```bash
# Start the Kafka broker service
$ bin/kafka-server-start.sh config/server.properties
```

Once all services have successfully launched, you will have a basic Kafka environment running and ready to use.

### Step 3: Create a Topic
Before you can write your first data, you must create a topic. Open another terminal session and run:

```bash
$ bin/kafka-topics.sh --create --topic quickstart-events --bootstrap-server localhost:9092
```

All of Kafka's command line tools have additional options: run the `kafka-topics.sh` command without any arguments to display usage information.

### Step 3: Write Data into the Topic
Run the console producer client to write a few data into your topic. By default, each line you enter will result in a separate event being written to the topic.

```bash
$ bin/kafka-console-producer.sh --topic quickstart-events --bootstrap-server localhost:9092
This is my first event
This is my second event
```

You can stop the producer client with `Ctrl-C` at any time.

### Step 4: Read the Data
Open another terminal session and run the console consumer client to read the events you just created:

```bash
$ bin/kafka-console-consumer.sh --topic quickstart-events --from-beginning --bootstrap-server localhost:9092
This is my first event
This is my second event
```

You can stop the consumer client with `Ctrl-C` at any time.

### Step 5: Terminate the Kafka Enviroment
Stop the producer and consumer clients with `Ctrl-C`, if you haven't done so already.

Stop the Kafka broker with `Ctrl-C`.

Lastly, if the Kafka with ZooKeeper section was followed, stop the ZooKeeper server with `Ctrl-C`.

If you also want to delete any data of your local Kafka environment including any events you have created along the way, run the command:

```bash
$ rm -rf /tmp/kafka-logs /tmp/zookeeper /tmp/kraft-combined-logs
```

## SpringBoot Kafka