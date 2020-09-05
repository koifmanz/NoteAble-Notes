---
tags: [Notebooks/AirFlow]
title: Hooks
created: '2020-09-05T03:44:57.084Z'
modified: '2020-09-05T05:06:42.987Z'
---

# Hooks

### What are hooks?

Hooks are the method via we can have connections to other systems and databases, and the are reusable and secure. 
AirFlow come with many Hooks that can integrate with common systems like:

* HttpHook
* PostgresHook (works with RedShift)
* MySqlHook

and more...

Example:

```python
from airflow import DAG
from airflow.hooks.postgres_hook import PostgresHook
from airflow.operators.python_operator import PythonOperator


def load():
  # create a Postgres Hook option using the demo connection
  db_hook = PostgresHook('demo')
  df = db_hook.get_pandas_df('SELECT * FROM rides')
  print(f'Complete, return {len(df)} records')

load_task = PythonOperator(task_id='load', python_callable=load,...)
```

### How to create a connection using the GUI

This will show how to create connection to AWS service, but there a lot of connection that one can already use.

1. open your browser to *localhost:8080* and open *Admin -> Variables*
2. Click *Create*
3. Set the following variables: 
    * *Key* equal to "s3_bucket"
    * set *Val* equal to "udac-data-pipelines"
4. Click *Save*
5. Open *Admin -> Connections*
6. Click *Create*
7. Set the following variables:
    * *Conn Id* to "aws_credentials", *Conn Type* to Amazon Web Services (this is a choice box) 
    * *Login* to your aws_access_key_id and *Password* to your aws_secret_key
8. click *Save*
9. Run the DAG

### S3 to Redshift DAG Demo

Hooks are the method via we can have connections to other systems and databases, and the are reusable and secure. 
AirFlow come with many Hooks that can integrate with common systems like:


```python
from airflow import DAG
from airflow.hooks.postgres_hook import PostgresHook
from airflow.operators.python_operator import PythonOperator

import sql # sql in this case is a file with quries and etc.

def load_data_to_redshift(*args, **kwargs):
  aws_hook AwsHook("aws_credential")
  credentials = aws_hook.get_credentials()
  redshift_hook = PostgresHook("redshift")
  sql_stmt = sql.COPY_STATIONS_SQL.format(credentials.access_key, credentials.secret_key)

dag = DAG(
  'lesson1.demo6',
  start+date=datetime.datetime.now())

create_table = PostgresOperator(
  task_id='create_table',
  postgres_conn_id='<REPLACE>', # create using admin -> connection
  sql=sql.CREATE_STATIONS_TABLE_SQL, # sql in this case is a file with create statment
  dag=dag
)

copy_task = PythonOperator(
  task_id='copy_to_redshift',
  dag=dag,
  python_callable=load_data_to_redshift
)

create_table >> copy_task
```


