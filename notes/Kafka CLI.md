---
tags: [Notebooks/DataStreaming]
title: Kafka CLI
created: '2021-03-04T08:51:52.586Z'
modified: '2021-09-07T05:05:45.961Z'
---

# Kafka CLI


### Get help about command

Just enter the command.

```shell
kafka-topics
```

### list all Kafka topics

underscore topics are system topics, so be aware. host:port need to be change to relveant location.
In the newer version use --bootstrap-server insted of --zookeeper.

```shell
kafka-topics --list --zookeeper host:port
```

Adding the switch --topic "name" will return a snimgle topic by that name.


### Create new topic

* --topic name = tells Kafka what to name the topic
* --partitions 1 = more will be written here
* --replication-factor 1 = more will be written here


```shell
kafka-topics --create --topic "name" --partitions 1 --replication-factor 1 --zookeeper host:port
```

### Producing data

* --broker-list replace zookeeper, in a sense
* One will be able to write messages in the cli.


```shell
kafka-console-producer --topic "name" --broker-list localhost:9092
```

### Consuming data

* --bootstrap-server replace --broker-list
* same host:port as the prudocer, not as kafka-topics
* --from-beginning make it so we will see all messages, not only new.


```shell
kafka-console-consumer --topic "name" --bootstrap-server localhost:9092 --from-beginning
```

### Deleting topics


```shell
kafka-topics --delete --topic "name" --zookeeper host:port
```
