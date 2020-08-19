---
tags: [Notebooks/GDAL]
title: Setup
created: '2019-12-10T08:05:05.257Z'
modified: '2020-08-19T06:40:18.314Z'
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


### Install on Win10 with Conda

On Windows, because conda-forge relies on some package built with defaults blas (like scipy) one must use the defaults channel on top of conda-forge and activate conda's new strict channel feature.

One can do that with:

```shell
conda config --add channels conda-forge
conda config --add channels defaults
conda config --set channel_priority strict
```
[github: gdal-feedstock](https://github.com/conda-forge/gdal-feedstock/issues/269)
