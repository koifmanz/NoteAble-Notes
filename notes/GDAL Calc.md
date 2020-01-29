---
tags: [Notebooks/GDAL]
title: GDAL Calc
created: '2019-12-16T06:30:25.976Z'
modified: '2019-12-16T06:33:44.424Z'
---

# GDAL Calc


### Re-classify raster values
Roads Give higher score to nearer pixels:
* 0-1000m  --> 100
* 1000-5000m --> 50
* 5000m and above --> 10
```shell
 gdal_calc -A roads_proximity.tif --outfile roads_class.tif /
  --calc="100*(A<=1000) + 50*(A>1000)*(A<=5000) + 10*(A>5000)" 
```

### Computing NDVI
It is important to set nodata value.
```shell
 gdal_calc -A -A landsat8/RT_LC08_L1TP_137042_20190920_20190926_01_T1_2019-09-20_B5.TIF /
 -B landsat8/RT_LC08_L1TP_137042_20190920_20190926_01_T1_2019-09-20_B4.TIF /
 --outfile ndvi.tif --calc="(A-B)/(A+B)" --NoDataValue=-999
```

