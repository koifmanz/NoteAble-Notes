---
attachments: [Clipboard_2021-09-20-09-09-20.png, Clipboard_2021-09-20-09-15-35.png]
tags: [Notebooks/DesignDataApp]
title: 03-2 - Storage and Retrival - Btrees
created: '2021-09-18T06:54:25.216Z'
modified: '2021-09-20T09:41:23.974Z'
---

#  03-2 - Storage and Retrival - Btrees

### B-Trees

The most widely used indexing structure. B-trees have stood the test of time very well (since 1970). They remain the standard index implementation in almost all relational databases, and many nonrelational databases use them too.

#### How?

B-trees keep key-value pairs sorted by key, which allows efficient key-value lookups and range queries.  In contrast to SSTables, B-trees break the database down into fixed-size blocks or **pages**, traditionally 4 KB in size, and read or write one page at a time.
This design is corresponds more to the hardware, because disks are also working in fixed size blocks.  

Each page have an location or adress, which allow one page to refer another (like a pointer), but this on the disk and not on memory. The page refernce can work in kind of a tree like this:

![](@attachment/Clipboard_2021-09-20-09-09-20.png)

1. the top page use as root, it a refernce to all other pages
2. then there is a child which refernce to the leaf pages
3. the leaf page containing individual keys, and it have the value of a refernce to the page which have the value.

If there isn’t enough free space in the page to accommodate the new key, it is split into two half-full pages, and the parent page is updated to account for the new subdivision of key ranges, like the following example:

![](@attachment/Clipboard_2021-09-20-09-15-35.png)

#### Good sides?

* B-Tree algorithm ensures that the tree remains balanced, a B-tree with n keys always has a depth of O(log n).
* Most databases can fit into a B-tree that is three or four levels deep, so you don't need to follow many references.


#### Beware!?

* If database crash while the pages updateing/overwritten -> corrupted index
* It is assumed that the overwrite does not change the location of the page

To solve this it is common for B-tress to include an additional data structure on disk. This is an append-only file to which every B-tree modification must be written before it can be applied to the pages of the tree itself. Because B-Trees are old there a lot of solutions for them. 

### LSM vs B-Trees

* LSM-trees are typically faster for writes, whereas B-trees are thought to be faster for reads.

#### LSM-Trees Advantages

* A B-tree index must write every piece of data at least twice: once to the write-ahead log, and once to the tree page itself.
* Also a B-Tree need to write an entire page at a time, and sometimes more then one time at a time (depand on the engine).
* write amplification - one write to the database resulting in multiple writes to the disk over the course of the database’s lifetime.
  * the more that a storage engine writes to disk, the fewer writes per second it can handle within the available disk bandwidth.
  * LSM-trees are typically able to sustain higher write throughput, this important in magnetic hard drive (there order writing is better than random).
* LSM-trees can be compressed better, and thus often produce smaller files.
* B-tree storage engines leave some disk space unused due to fragmentation.

#### LSM-Trees Downsides

* the compaction process can sometimes interfere with the performance of ongoing reads and writes. The impact on throughput and average
response time is usually small, but at higher percentiles. B-Trees can be more predictable.
* issue with compaction arises at high write throughput.
* In B-trees is that each key exists in exactly one place in the index, whereas a log-structured storage engine may have multiple copies of the same key in different segments. good for strong transactional semantics.
  







