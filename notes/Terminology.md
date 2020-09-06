---
tags: [Notebooks/AirFlow]
title: Terminology
created: '2020-09-03T08:38:17.976Z'
modified: '2020-09-06T11:21:25.107Z'
---

# Terminology

### What is Data Pipleine?

A series of steps in which data is processed, and probaly have a schedule.

### ELT vs ETL

ETL is normally a continuous, ongoing process with a well-defined workflow. ETL first extracts data from homogeneous or heterogeneous data sources. Then, data is cleansed, enriched, transformed, and stored either back in the lake or in a data warehouse.

ELT (Extract, Load, Transform) is a variant of ETL wherein the extracted data is first loaded into the target system. Transformations are performed after the data is loaded into the data warehouse. ELT typically works well when the target system is powerful enough to handle transformations. Analytical databases like Amazon Redshift and Google BigQ. We first uplaod all the raw data and then work with it, and go with data lakes.

*Source: [xplenty](https://www.xplenty.com/blog/etl-vs-elt/)*


### Data Validation

The process of ensuring that data is present, correct and meaningful. Make sure we will got the right result and our data is good.


### DAGs - Directed Acyclic Graphs

Thats the way data pipelines are expressed, a idea help describe them. work like network, with nodes (users for example) and edges (relationships). DAG is not a cycle because they have a direction.

In ETL is step is a node. and the step depand on the prior steps.

<p align="center">
  <img src="https://video.udacity-data.com/topher/2019/February/5c5f5b00_capture/capture.png" width="700">
</p>

* Nodes: A step in the data pipeline process.
* Edges: The dependencies or relationships other between nodes.

### What is AirFlow? How it works?

An open source tool which structures data pipelines as DAGs. WorkFlow based on 5 compentents:

* Scheduler - The time manager.
* Work Queue - used by the scheduler to deliver tasks that need to be run to the worker.
* Worker - take a task from the work queue and process it. When task is finished take another one.
* Database - save all the metadata of the process.
* Web Interface - a GUI/Dashboard to monitor and managing the ETL. 

<p align="center">
  <img src="https://video.udacity-data.com/topher/2019/February/5c5f8e1d_how-airflow-works/how-airflow-works.png" width="700">
</p>

#### The Steps:

1. The Airflow Scheduler starts DAGs based on time or external triggers.
2. Once a DAG is started, the Scheduler looks at the steps within the DAG and determines which steps can run by looking at their dependencies.
3. The Scheduler places runnable steps in the queue.
4. Workers pick up those tasks and run them.
5. Once the worker has finished running the step, the final status of the task is recorded and additional tasks are placed by the scheduler until all tasks are complete.
6. Once all tasks have been completed, the DAG is complete.


### Schedules

AirFlow determine the schedule based on the star date, end date and the interval (monthly, hourly, etc.). Whilte start date is a must, end date and the interval are not (it will run once a day as default). 

##### Start Date

Airflow will begin running pipelines on the start date selected. Whenever the start date of a DAG is in the past, and the time difference between the start date and now includes more than one schedule intervals, Airflow will automatically schedule and execute a DAG run to satisfy each one of those intervals. This feature is useful in almost all enterprise settings, where companies have established years of data that may need to be retroactively analyzed.

##### End Date

Airflow pipelines can also have end dates. You can use an end_date with your pipeline to let Airflow know when to stop running the pipeline. End_dates can also be useful when you want to perform an overhaul or redesign of an existing pipeline. Update the old pipeline with an end_date and then have the new pipeline start on the end date of the old pipeline.

### AirFlow component summary

* DAG - A collection of nodes and edges that describe the order of operations for a data pipeline
* Task - An instantiated step in a pipeline fully parameterized for execution
* Hook - A reusable connection to an external database or system
* Operator - An abstract building block that can be configured to perform some work


