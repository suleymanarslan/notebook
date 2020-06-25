# Kafka 

Sources: 

* [Quickstart](https://kafka.apache.org/quickstart)
* [MSK Developer Guide](https://docs.aws.amazon.com/msk/latest/developerguide/create-topic.html)

## Download

```
$ wget https://archive.apache.org/dist/kafka/2.2.1/kafka_2.12-2.2.1.tgz
$ tar -xzf kafka_2.12-2.2.1.tgz
```

## Server:

Start Zookeeper

```
$ bin/zookeeper-server-start.sh config/zookeeper.properties
```

Start server:

```
$ bin/kafka-server-start.sh config/server.properties
```

## Topics

Create a topic:

```
$ bin/kafka-topics.sh --create --bootstrap-server localhost:9092 --replication-factor 1 --partitions 1 --topic test
```

Or pointing to Zookeeper on AWS:

```
$ bin/kafka-topics.sh --^Ceate --zookeeper z-1.kafka-prod.jra9w9.c4.kafka.eu-central-1.amazonaws.com:2181 --replication-factor 3 --partitions 1 --topic
 AWSKafkaTutorialTopic
```

List Topics:

```
$ bin/kafka-topics.sh --list --zookeeper z-1.kafka-prod.jra9w9.c4.kafka.eu-central-1.amazonaws.com:2181
```

