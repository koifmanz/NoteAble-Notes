---
tags: [Notebooks/AirFlow]
title: Production Data Pipelines
created: '2020-09-07T06:52:10.108Z'
modified: '2020-09-08T07:09:45.634Z'
---

# Production Data Pipelines

### Extanding Airflow - What are plugins?

Custom **operators** and **hooks** which can be reusable and community made. 
Airflow has a rich and vibrant open source community. This community is constantly adding new functionality and extending the capabilities of Airflow. As an Airflow user, you should always [check Airflow contrib](https://github.com/apache/airflow/tree/master/airflow/contrib) before building your own airflow plugins, to see if what you need already exists.

Operators and hooks for common data tools like Apache Spark and Cassandra, as well as vendor specific integrations for Amazon Web Services, Azure, and Google Cloud Platform can be found in Airflow contrib. If the functionality exists and its not quite what you want, that’s a great opportunity to add that functionality through an open source contribution.

They can be integrate by simply dropping files in your *$AIRFLOW_HOME/plugins folder*.

Examples:

* [github: Europython 2016](https://github.com/blue-yonder/airflow-plugin-demo)
* [Airflow docs](https://airflow.readthedocs.io/en/1.10.12/plugins.html)


### Task boundaries

DAG tasks should be designed such that they are:

* Atomic and have a single purpuse - like a function
* Maximize parallesim
* Make failure states obvius

That way we can have two great benefits; *Re-visitable* which help us understand the code even after some time. The second benefit is the *paralleizion*, which will speed up the execution time.  

### Monitoring

Airflow can surface metrics and emails to help you stay on top of pipeline issues. There are few built in tools:

1. SLA (browser menu) -  Airflow DAGs may optionally specify an SLA, or “Service Level Agreement”, which is defined as a time by which a DAG must complete. For time-sensitive applications these features are critical for developing trust amongst your pipeline customers and ensuring that data is delivered while it is still meaningful. Slipping SLAs can also be early indicators of performance problems, or a need to scale up the size of your Airflow cluster.
2. Emails and Alerts - Airflow can be configured to send emails on DAG and task state changes. These state changes may include successes, failures, or retries. Failure emails can allow you to easily trigger alerts. It is common for alerting systems like PagerDuty to accept emails as a source of alerts. If a mission-critical data pipeline fails, you will need to know as soon as possible to get online and get it fixed.
3. Metrics - Airflow comes out of the box with the ability to send system metrics using a metrics aggregator called statsd. Statsd can be coupled with metrics visualization tools like Grafana to provide you and your team high level insights into the overall performance of your DAGs, jobs, and tasks. These systems can be integrated into your alerting system, such as pagerduty, so that you can ensure problems are dealt with immediately. These Airflow system-level metrics allow you and your team to stay ahead of issues before they even occur by watching long-term trends.

### Example for full DAG without plugins

```python
import datetime
import logging

from airflow import DAG
from airflow.hooks.postgres_hook import PostgresHook

from airflow.operators.postgres_operator import PostgresOperator
from airflow.operators.python_operator import PythonOperator

def log_oldest():
    redshift_hook = PostgresHook("redshift")
    records = redshift_hook.get_records("""
        SELECT birthyear FROM older_riders ORDER BY birthyear ASC LIMIT 1
    """)
    if len(records) > 0 and len(records[0]) > 0:
        logging.info(f"Oldest rider was born in {records[0][0]}")

def log_youngest():
    redshift_hook = PostgresHook("redshift")
    records = redshift_hook.get_records("""
        SELECT birthyear FROM younger_riders ORDER BY birthyear DESC LIMIT 1
    """)
    if len(records) > 0 and len(records[0]) > 0:
        logging.info(f"Youngest rider was born in {records[0][0]}")
     

dag = DAG(
    "lesson3.exercise2",
    start_date=datetime.datetime.utcnow()
)

load_and_analyze = PythonOperator(
    task_id='load_and_analyze',
    dag=dag,
    python_callable=load_and_analyze,
    provide_context=True,
)

create_oldest_task = PostgresOperator(
    task_id="create_oldest",
    dag=dag,
    sql="""
        BEGIN;
        DROP TABLE IF EXISTS older_riders;
        CREATE TABLE older_riders AS (
            SELECT * FROM trips WHERE birthyear > 0 AND birthyear <= 1945
        );
        COMMIT;
    """,
    postgres_conn_id="redshift"
)

log_oldest_task = PythonOperator(
    task_id="log_oldest",
    dag=dag,
    python_callable=log_oldest
)

create_youngest_task = PostgresOperator(
    task_id="create_younest",
    dag=dag,
    sql="""
        BEGIN;
        DROP TABLE IF EXISTS younger_riders;
        CREATE TABLE younger_riders AS (
            SELECT * FROM trips WHERE birthyear > 2000
        );
        COMMIT;
    """,
    postgres_conn_id="redshift"
)

log_youngest_task = PythonOperator(
    task_id="log_youngest",
    dag=dag,
    python_callable=log_youngest
)

create_bike_ridden_task = PostgresOperator(
    task_id="bike_ridden",
    dag=dag,
    sql=""" 
        BEGIN;
        DROP TABLE IF EXISTS lifetime_rides;
        CREATE TABLE lifetime_rides AS (
            SELECT bikeid, COUNT(bikeid)
            FROM trips
            GROUP BY bikeid
        );
        COMMIT;
    """,
    postgres_conn_id="redshift"
)

create_stations_count_task = PostgresOperator(
    task_id="stations_count",
    dag=dag,
    sql="""
        BEGIN;
        DROP TABLE IF EXISTS city_station_counts;
        CREATE TABLE city_station_counts AS(
            SELECT city, COUNT(city)
            FROM stations
            GROUP BY city
        );
        COMMIT;
    """,
    postgres_conn_id="redshift"
)

load_and_analyze >> create_oldest_task
create_oldest_task >> log_oldest_task
create_youngest_task >> log_youngest_task
```


