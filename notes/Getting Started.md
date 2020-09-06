---
tags: [Notebooks/AirFlow]
title: Getting Started
created: '2020-09-03T14:06:31.367Z'
modified: '2020-09-06T11:32:43.886Z'
---

# Getting Started

### Initialize

Every DAG must have 2 companents:

1. name (lesson1.demo1 in our example)
2. start date (in our case now function from datetime library)

```python
from airflow import DAG
from airflow.operators.python_operator import PythonOperator

import datetime
import logging

dag = DAG(
  'lesson1.demo1',
  start_date=datetime.datetime.now(), # can be replaced with a date -> datetime(2019, 2, 4)
  # start_date = datetime.datetime.now() - datetime.timedelta(days=30) 
  schedule_interval='@daily' # not required, you can use also @monthly or others
)
```

### Initialize with schedule

In the follwing case AirFlow will show us the ETL already run one month ago.

```python
dag = DAG(
  'lesson2.demo2',
  start_date = datetime.datetime.now() - datetime.timedelta(days=30),
  end_date = datetime.datetime(2022, 12, 1, 0, 0, 0, 0),  
  schedule_interval = '@monthly',
  max_active_runs = 1 # how much DAGs run at once, or each month will run alone
)
```

### Task / Node

Operators are the atomics steps of work that make up a DAG. greet_task in the code below is a task.

```python
def greet():
  logging.info("Hello World!")

greet_task = PythonOperator(
  task_id = "greet_task"
  python_callable = greet, # our founction from above
  dag = dag # see init process from Initialize section
)
```

There are a lot of built in operators, such as:

* PythonOperator
* PostgresOperator
* RedshiftToS3Operator
* S3ToRedshiftOperator
* BashOperator
* Sensor
* SimpleHttpOperator

### Dependencies

Task dependencies can be described in code  using >> and <<

* a >> b - means a comes before b
* a << b - means a comes after b

Example:

```python

# Define needed functions

def hello_world():
  logging.info("Hello World!")

def current_time():
  logging.info(f"Current time is {datetime.datime.utcnow().isoformat()}")

def working_dir():
  logging.info(f"Working directory is {os.getcwd}")

def complete():
  logging.info("Pipleline is now complete")

# init DAG

dag = DAG(
  'lesson3.demo3',
  start_date = datetime.datetime.now() - datetime.timedelta(days=1), 
  schedule_interval='@hourly')

# define tasks

hello_world_task = PythonOperator(
  task_id="hello_world",
  python_callable=hello_world,
  dag=dag)

current_time_task = PythonOperator(
  task_id="current_time",
  python_callable=current_time,
  dag=dag)

working_dir_task = PythonOperator(
  task_id="working_dir",
  python_callable=working_dir,
  dag=dag)

complete_task = PythonOperator(
  task_id="complete",
  python_callable=complete,
  dag=dag)

# configure the tasks dependencies and order

#
#                  -> current_time_task
#                 /                      \
# hello_world_task                        -> complete_task
#                 \                      /
#                  ->  working_dir_task             


hello_world_task >> current_time_task
hello_world_task >> working_dir_task
current_time_task >> complete_task
working_dir_task >> complete_task
```

### Templating with Context variables

AirFlow levrages templating to allow users to "fill in the blank" with important runtime variables tasks.

Example:

```python
from airflow import DAG
from airflow.operators.python_operator import PythonOperator

def hello_date(*args, **kwargs):
  print(f"Hello {kwargs['execution_date']}")

divvy_dag = DAG(...)

task = PythonOperator(
  task_id='hello_world'
  python_callable=hello_date,
  provide_context=True,
  dag=divvy_dag
)
```

In the code above *kwargs[execution_date]* come from *provide_context=True*, which come from AirFlow itself. 

*Read More: [godatadriven.com](https://godatadriven.com/blog/the-zen-of-python-and-apache-airflow/)*


