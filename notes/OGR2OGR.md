---
tags: [Notebooks/GDAL]
title: OGR2OGR
created: '2019-12-09T09:19:10.051Z'
modified: '2019-12-09T11:55:23.995Z'
---

# OGR2OGR


### Shapefile to CSV with XY
One can replace AS_XY to others formats. I don't think the flag -overwrite is must 
```
 ogr2ogr -f "CSV" -overwrite -lco GEOMETRY=AS_XY MyLayer2.csv MyLayer.shp 
```

[gis.stackexchange](https://gis.stackexchange.com/questions/203329/ogr2ogr-keep-geometry-when-converting-to-csv)


### CSV to shapefile
 
 Make sure to replace EPSG and xy fields names.

```
 ogr2ogr -s_srs EPSG:4326 -t_srs EPSG:3857 -oo X_POSSIBLE_NAMES=Lon* -oo Y_POSSIBLE_NAMES=Lat*  -f "ESRI Shapefile" test.shp test.csv
```

For more than one file and unix shell see the code below. It maybe won't work in windows cmd, but will in CMDer.

```
for f in *.csv ; do echo $f ${f%csv}shp ; done
```

* echo = command 
* $f / ${f%csv}shp - vars for the csv and shpefile.

Example:
```
for /R %f in (*.csv) do ogr2ogr -s_srs EPSG:4326 -t_srs EPSG:4326 -oo X_POSSIBLE_NAMES=Lon* -oo Y_POSSIBLE_NAMES=Lat* -f "ESRI Shapefile" "%~dpnf.shp" %f
```

[gis.stackexchange](https://gis.stackexchange.com/questions/276590/bulk-csv-to-shapefile-using-ogr2ogr)


