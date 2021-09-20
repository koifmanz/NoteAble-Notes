---
tags: [Notebooks/DataStreaming]
title: Producers
created: '2021-03-05T08:06:07.160Z'
modified: '2021-03-05T08:36:25.622Z'
---

# Producers


### Synchronous Production vs Asynchronous Production

Synchronous production is the simplest type of unit, work until the message recipt has been confirmed. It is a rare in Kafka world, but great for cases like when need confimration about cerdit card, etc. When data loss cannot be happend.

Asynchronous Production send the data and immediatly continue to work.


### Producer Configuration Options - Summary

* All available settings for the confluent_kafka_python library can be found in the librdkafka configuration options. confluent_kafka_python uses librdkafka under the hood and shares the exact configuration options in this document.
* It is a good idea to always set the client.id for improved logging, debugging, and resource limiting
* The retries setting determines how many times the producer will attempt to send a message before marking it as failed
* If ordering guarantees are important to your application and you’ve also enabled retries, make sure that you set enable.idempotence to true
* Producers may choose to compress messages with the compression.type setting
    1. Options are none, gzip, lz4, snappy, and zstd
    2. Compression is performed by the producer client if enabled
    3. If the topic has its own compression setting, it must match the producer setting, otherwise the broker will decompress and recompress the message into its configured format.
    4. The acks setting determines how many In-Sync Replica (ISR) Brokers need to have successfully received the message from the client before moving on
    5. A setting of -1 or all means that all ISRs will have successfully received the message before the producer proceeds
    6. Clients may opt to set this to 0 for performance reasons

