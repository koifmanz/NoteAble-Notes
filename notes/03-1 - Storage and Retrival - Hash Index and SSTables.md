---
attachments: [Clipboard_2021-09-18-09-29-38.png]
tags: [Notebooks/DesignDataApp]
title: 03-1 - Storage and Retrival - Hash Index and SSTables
created: '2021-09-18T06:20:51.798Z'
modified: '2021-09-20T10:10:04.527Z'
---

# 03-1 - Storage and Retrival - Hash Index and SSTables

### Index - data structure that power the database

In order to efficiently find the value for a particular key in the database, we need a different data structure: an index. the general idea
behind them is to keep some additional metadata on the side, which acts as a signpost and helps you to locate the data you want. If you want to search the same data in several different ways, you may need several different indexes on different parts of the data.

well-chosen indexes speed up read queries, but every index slows down writes.


#### When not?

* **Heap file** - place where rows are stored (without order) when there are more then 1 index. then all the index refernce to same place, less files.

The following cases explain when the index in this chapter are not fit:

* **concatenated index** - simply combines several fields into one key by appending one column to another, like last name-first name in phone book. one type of multi-column index. This is important for geospatial data, which require sometime range queires. here b-trees and LSM-Trees are not fit.
* **Fuzzy querying** - looking for data that have similar keys.
* **Memory storing** - good for (very) small databases, they can be faster because they can avoid the overheads of encoding in-memory data structures in a form that can be written to disk.


### Hash indexes

Works like dictionary, it keep an in-memory hash map where every key is mapped to a byte offset in the data file. writing new row update the hash map, and when we look for data it use the hash to find the offset, seek the data and read it.

![](@attachment/Clipboard_2021-09-18-09-29-38.png)

A storage engine like Bitcask (store key:value and hash map in the RAM) is well suited to situations where the value for each key is updated frequently. 
to  avoid running out of disk space one can break the log file into segmant by certain size, close it when it reach the limit and perform compaction (remove duplicate keys in the log). 

#### log file issues:

* file format - binary is better then csv. a binary format that first encodes the length of a string in bytes, followed by the raw string.
* deleting records - to delete a key and its value one need to append a special deletion record to the data file.
* crash recovery - If the database is restarted, the in-memory hash maps are lost. 
* partially written records - for example database may crash at any time, for example when you halfway through appending a record to the log.
* concurrency control - Data file segments are append-only and otherwise immutable, so they can be read concurrently by multiple threads.

#### append-only log good sides:

* Appending and segment merging are sequential write operations, which are generally much faster than random writes.
* Concurrency and crash recovery are much simpler if segment files are append-only or immutable.
* Merging old segments avoids the problem of data files getting fragmented over time.

#### append-only log limitations:

* The table must fit in memory (RAM).
* It is not easy to make hash table work on disk (because of I/O).
* Range queries are not efficient.

### SSTable?

**Sorted String Table = SSTable**

Taking hashmap and:

* sorting it by key
* each key only appers once in each merged segment

#### advantages over hash index

* Merging segments is simple and efficient, even if the files are bigger than the available memory.
* to find a particular key in the file, you no longer need to keep an index of all the keys in memory. you can have lower number of key in the memory thanks to the ordering).
* Since read requests need to scan over several key-value pairs in the requested range anyway, it is possible to group those records into a block and compress it before writing it to disk. Each entry of the sparse in-memory index then points at the start of a compressed block. It will reduce disk space and (the comperssion) I/O bandwidth.

#### LSM-Trees?

keeping a cascade of SSTables that are merged in the background, and since data is stored in sorted order, you can efficiently perform range queries (scanning all keys above some minimum and up to some maximum), and because the disk writes are sequential the LSM-tree can support remarkably high write throughput.





