---
tags: [Notebooks/GDAL]
title: GDAL Translate
created: '2019-12-10T08:39:59.751Z'
modified: '2019-12-15T08:38:28.501Z'
---

# GDAL Translate


### Landsat Pan Sharpening
1. use band 8 on your rgb raster
```shell
gdal_pansharpen landsat8/RT_LC08_L1TP_137042_20190920_20190926_01_T1_2019-09-20_B8.TIF /
rgb.tif pansharpened.tif -r bilinear -co COMPRESS=DEFLATE -co PHOTOMETRIC=RGB
```
2. use gdal translate to scale and strech
```shell
gdal_translate -scale 0 0.3 0 255 -exponent 0.5 -ot Byte -a_nodata 0 /
pansharpened.tif pansharpened_stretch.tif
```
