---
tags: [Notebooks/DataStreaming]
title: Topics
created: '2021-03-05T06:32:27.795Z'
modified: '2021-03-05T07:05:18.132Z'
---

# Topics

### Data Management - Key Points

1. Data retention determines how long Kafka stores data in a topic. *The retention.bytes*, *retention.ms settings* control retention policy
2. When data expires it is deleted from the topic. This is true if *cleanup.policy* is set to *delete*.
3. Retention policies may be time based. Once data reaches a certain age it is deleted. *The retention.ms* setting controls retention policy on time.
4. Retention policies may be size based. Once a topic reaches a certain age the oldest data is deleted. The *retention.bytes* setting controls retention policy on size.
5. topics can be compacted in which there is no size or time limit for data in the topic. This is true if *cleanup.policy* is set to *compact*.
6. Compacted topics use the message key to identify messages uniquely. If a duplicate key is found, the latest value for that key is kept, and the old message is deleted. In this case older rcords will be deleted based on keys.
7. **Kafka topics should store data for one type of event, not multiple types of events.**


### Partitioning Topics tips

1. partitions number depand on the case.
2. One can add partitions at later date by alter the topic.
3. Partitions have performance consequences. They require additional networking latency and potential rebalances, leading to unavailability.
4. The order of messages are only between messages in the partition.


### Partitioning Topics Equation

Determine the number of partitions you need by dividing the overall throughput you want by the throughput per single consumer partition or the throughput per single producer partition. Pick the larger of these two numbers to determine the needed number of partitions. 


```shell
Partitions = Max(Overall Throughput/Producer Throughput, Overall Throughput/Consumer Throughput)
```

*For exmaple -*  3 Producers and 5 Consumers, each operating at 10MB/s per single producer/consumer partition, and desired throughput of 100mb:


```shell
Max(100MBs/(3 * 10MB/s), 100MBs/(5 * 10MB/s)) = Max(2) ~= *4 partitions needed*
```
*This is little more complex then the equation above*


[Considerations in choosing the number of partitions](https://www.confluent.io/blog/how-choose-number-topics-partitions-kafka-cluster/)
