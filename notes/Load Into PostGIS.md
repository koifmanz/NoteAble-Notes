---
tags: [Notebooks/Postgres and postgis]
title: Load Into PostGIS
created: '2019-12-08T10:30:04.089Z'
modified: '2020-09-07T16:35:41.895Z'
---

# Load Into PostGIS

### From GeoPandas

```python
from geoalchemy2 import Geometry, WKTElement
from sqlalchemy import *
import pandas as pd
import geopandas as gpd

# Creating SQLAlchemy's engine to use
engine = create_engine('postgresql://username:password@host:socket/database')


geodataframe = gpd.GeoDataFrame(pd.DataFrame.from_csv('<your dataframe source>'))
#... [do something with the geodataframe]

geodataframe['geom'] = geodataframe['geometry'].apply(lambda x: WKTElement(x.wkt, srid=<your_SRID>)

#drop the geometry column as it is now duplicative
geodataframe.drop('geometry', 1, inplace=True)

# Use 'dtype' to specify column's type
# For the geom column, we will use GeoAlchemy's type 'Geometry'
geodataframe.to_sql(table_name, engine, if_exists='append', index=False, 
                         dtype={'geom': Geometry('POINT', srid= <your_srid>)}) 
```

[StackOverflow](https://gis.stackexchange.com/questions/239198/adding-geopandas-dataframe-to-postgis-table)


### From GDB using GDAL

```
ogr2ogr -f "PostgreSQL" PG:"host=servername port=5432 user='username' password='password' dbname='PostGISDBName'" gdb-path -overwrite -progress --config PG_USE_COPY YES
```

[Cadlinecommunity](https://www.cadlinecommunity.co.uk/hc/en-us/articles/360000633269-PostGIS-How-do-you-import-an-ESRI-Geodatabase-into-PostGIS-)


### Insert Data using SQL

```SQL
INSERT INTO <table> (field 1…, field n, <geom field>) 
VALUES (value 1… value n, ST_SetSRID(ST_MakePoint(X , Y), SRID));
```

[stackexchange](https://gis.stackexchange.com/questions/104607/problem-with-geometry-srid-in-postgis)

### Insert Data using shp2pgsql

```python
import os
import subprocess

cmd = 'shp2pgsql -s 4326 ../data/shp/statistical_neighborhoods.shp temp_table | psql -h hostname -d databasename -U username --quiet'

subprocess.call(cmd, shell=True)
```

[stackexchange](https://gis.stackexchange.com/questions/251386/how-to-run-shp2pgsql-in-python-without-reporting-every-row-loaded)
