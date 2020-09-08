---
tags: [Notebooks/Postgres and postgis]
title: Connect to DB
created: '2020-09-07T16:00:14.860Z'
modified: '2020-09-07T16:09:35.190Z'
---

# Connect to DB

### Create a docker container

```bash
docker run --name postgis -d -e POSTGRES_USER=ziv -e POSTGRES_PASS=password -e POSTGRES_DBNAME=gis -e ALLOW_IP_RANGE=<*> -p 5433:5432 -v pg_data:/var/lib/postgresql kartoza/postgis
```

* *--name my_postgis* - The name my_postgis is arbitrary. You can use another name for the image.
* *-p 5433:5432* - The PostgreSQL server must listen on a specific port for client connections. 5432 is the default Postgres port. We are using 5433 in case we actually have or ever install a native Postgres server. 5433 is mapped to port 5432 in the container.
* *-v pg_data*- /var/lib/postgresql maps the location of the data cluster in the container (/var/lib/postgresql) to the docker volume created before.

##### Create pg_data



```bash
docker volume create pg_data
```

### Connect to Qgis or Dbeaver (local)

<p align="center">
  <img src="https://sites.temple.edu/spatialdb/files/2019/09/DbeaverDockerConnectionSettings.png" width="700">
</p>

*Source: [temple.edu](https://sites.temple.edu/spatialdb/2019/09/04/creating-a-postgis-server-in-docker/)*
*Source: [docker hub: kartoza/docker-postgis](https://github.com/kartoza/docker-postgis)*
