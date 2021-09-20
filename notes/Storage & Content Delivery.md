---
tags: [Notebooks/AWS]
title: Storage & Content Delivery
created: '2020-10-20T09:31:50.271Z'
modified: '2020-10-20T10:23:48.619Z'
---

# Storage & Content Delivery

### S3

Can store anything. organize by buckets:
* have globally unique names
* live in a region
* can hold millions of objects

have few storage classes - Glacier for example is the cheapest and best for data archiving.

### DynamoDB

DynamoDB is a NoSQL document database service that is fully managed. Unlike traditional databases, NoSQL databases, are schema-less. Schema-less simply means that the database doesn't contain a fixed (or rigid) data structure.

Few points:

* can handle more than 10 trillion requests per day and quickly scale.
* is serverless as there are no servers to provision, patch, or manage.
* supports key-value and document data models. 
* The data store as JSON.
* synchronously replicates data across three AZs in an AWS Region.
* supports GET/PUT operations using a primary key.

### Relational Database Service (RDS)

RDS (or Relational Database Service) is a service that aids in the administration and management of databases. RDS assists with database administrative tasks that include upgrades, patching, installs, backups, monitoring, performance checks, security, etc. Between the service are: PostgresSQL, Oracle and more.

### Redshift 

Redshift is a cloud data warehousing service to help companies manage big data. Redshift allows you to run fast queries against your data using SQL, ETL, and BI tools. Redshift stores data in a column format to aid in fast querying.

* Redshift Spectrum is a feature that enables you to run queries against data in Amazon S3.
* Redshift clusters can be isolated using Amazon Virtual Private Cloud (VPC).
* It less than ideal for processing day-to-day transactions. A data warehouse is used for reporting and data analysis.


### Cloud Front

CloudFront is used as a global content delivery network (CDN). Cloud Front speeds up the delivery of your content through Amazon's worldwide network of mini-data centers called Edge Locations. If the the data is not in the edge it pull the data from the origin.

CloudFront works with other AWS services, as shown below, as an origin source for your application:

* S3
* Elastic Load Balancing
* EC2
* Lambda@Edge
* Shield

One can access it under Networking & Content Delivery section on the AWS Management Console.

