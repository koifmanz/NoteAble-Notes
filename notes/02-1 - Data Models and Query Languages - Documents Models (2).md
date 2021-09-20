---
tags: [Notebooks/DesignDataApp]
title: 02-1 - Data Models and Query Languages - Documents Models
created: '2021-09-08T12:37:17.031Z'
modified: '2021-09-20T05:59:00.094Z'
---

# 02-1 - Data Models and Query Languages - Documents Models

### NoSQL

Today NoSQL meaning is *Not Only SQL*, but it start as a catchy hastag for a meetup on open source, distributed nonrelational databases.
There several driving forces behind the adoption of NoSQL:

* A need for greater scalability, including very large datasets or very high write throughput.
* preference for free and open source software
* Specialized query operations that are not well supported by the relational model.
* Frustration with the restrictiveness of relational schemas, and a desire for a more dynamic and expressive data model, schema-on-read.

document-like structure can be for example a tree of one-to-many relationships.

The NoSQL world diverged in two main directions:

1. document databases - where the relationships between one document and another are rare.
2. graph databases - where the data is highly interconnected.

#### Document databases Characteristics

* Schema-On-Read: the structure of the data is implicit, and only interpreted when the data is read, similar to python. The difference between the approaches is particularly noticeable in situations where an application wants to change the format of its data. for example In documents db you will start writing new docuemnts and have an appliction code which handle old cases.
* data locality: only applies if you need large parts of the document at the same time (for example MongoDB BSON, a binary variant). Because even if you need small changes it sometimes still read all the document, it is better to use small documents.

#### Object-Relational Mismatch

Today a lot of development is done using object oriented programming languages, which leads to a common criticism of the SQL. If the data stored in relational table, an awkward translation is needed (between db and object in app code). ORM (m for mapping) help with it but not solve it. 

JSON model can solve some problem, because the lack of a schema:
* The information can be in one place, while in the rationl model you probably use joins or more than one query 
* One to many relationships can be stored in a tree like structure. 


#### When to use what?

* If the data in the appliction has a document like structure ==> document model:

  In this case it may be that the relational model will lead to cumbersome schemas and unnecessarily complicated application code. On the other hand too complicated nesting can lead to issues.

* Many-to-many ==> docuemnt model can lead to significantly more complex code:

  One can use denormalizing instead of joins, but then the appliction code will do more (which slower than a join). In document databases, joins are not needed for one-to-many tree structures, and support for joins is often weak. you have to emulate a join in application code by making multiple queries to the database. One need to remember that data has a tendency of becoming more interconnected with time (or development).

* a need for schema-on-read because:
   * There are many different types of objects, and it is not practical to put each type of object in its own table.
   * The structure of the data is determined by external systems over which you have no control and which may change at any time.

* For highly interconnected data ==> the document model is awkward, the relational model is acceptable, and graph models are the most natural.

 


