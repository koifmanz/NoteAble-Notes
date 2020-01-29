---
tags: [Notebooks/GDAL]
title: Setup
created: '2019-12-10T08:05:05.257Z'
modified: '2019-12-16T08:31:19.511Z'
---

# Setup


### Setting up Environmental Variables for Win10

Usefull tool to minimize tiff 3 bands raster size

```shell
//64 bit
setx PATH “%PATH%;C:\OSGeo4W64\bin”
setx GDAL_DATA “C:\OSGeo4W64\share\gdal”

//32 bit
setx PATH “%PATH%;C:\OSGeo4W\bin”
setx GDAL_DATA “C:\OSGeo4W\share\gdal”
```
[gisforthought](https://gisforthought.com/setting-up-your-gdal-and-ogr-environmental-variables/)


### Setting up Python3 for OSGeo4W shell

Just run py3_env which sets the shell up for Python 3 automatically, then run python3.

```shell
# py3_env
# python3
```
[gis.stackexchange](https://gis.stackexchange.com/questions/273870/osgeo4w-shell-with-python3)
