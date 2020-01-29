---
tags: [Notebooks/GDAL]
title: Rasters Compressions And Overviews
created: '2019-12-08T09:35:18.151Z'
modified: '2020-01-19T13:31:12.247Z'
---

# Rasters Compressions And Overviews


### GeoTiff Compression

Usefull tool to minimize tiff 3 bands raster size

```
gdal_translate -co COMPRESS=JPEG -co PHOTOMETRIC=YCBCR -co TILED=YES in.tif out.tif
```
[Cleverelephant](http://blog.cleverelephant.ca/2015/02/geotiff-compression-for-dummies.html)


### Create Virtual Dataset (VRT)

An xml file with relative links to all files. This follwing method allow you to create dataset for all files in folder:
 
```cmd
gdalbuildvrt all_ecw.vrt *.ecw -a_srs "EPSG:27700"
```

### Create Overview 

```cmd
gdaladdo -r average in.tif out.tif 2 4 8 16
```

little more advanced, which will create an external overview:

```cmd
gdaladdo -ro --config COMPRESS_OVERVIEW JPEG --config PHOTOMETRIC_OVERVIEW YCBCR --config INTERLEAVE_OVERVIEW PIXEL --config BIGTIFF_OVERVIEW YES in.vrt 2 4 8 16
 ```
[astuntech.atlassian]( https://astuntech.atlassian.net/wiki/spaces/ISHAREHELP/pages/14844053/Mosaic+thousands+of+raster+images)

Generally nearest neighbor technique is most suitable for discrete rasters since it will not change the values of the
cells. The average, gauss, and cubic techniques are more suitable for continuous rasters such as this DEM. They
will cause some smoothing of the data and may result in some values that are beyond the original range.

Source: discover QGIS 3.x, Kurt Menke, chpater 2 Exercice 7.



