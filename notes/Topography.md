---
tags: [Notebooks/GDAL]
title: Topography
created: '2019-12-08T10:53:57.069Z'
modified: '2019-12-08T13:07:52.167Z'
---

# Topography

### Create Contour Layer

Change n for contour lines, 10.0 e.g. Faster than arcgis or QGIS

```
gdal_contour -a <Target field name> soruce.tif contour.shp -i n
```
[gdal.org](https://www.gdal.org/gdal_contour.html)


### Create Hillshade
1. Build VRT file

```
gdalbuildvrt vrt_output.vrt raster_source1 raster_source2 
```
2. Create geotiff
```
gdal_translate -of GTiff vrt_output.vrt tiff_output1.tif
```
3. Project
```
gdalwarp -s_srs EPSG:4269 -t_srs EPSG:2228 -te xmin ymin xmax ymax-r bilinear
tiff_output.tif proj_output.tif
```
4. HillShade
```
gdaldem hillshade -az 45 -z 1.3 proj_output.tif hillshade_output.tif
```
  * -az flag is for the light direction and the -v flag is for vertical exaggeration. These may be changed as desired.
  * Generally, the smaller the scale of the map the more vertical exaggeration you would want to use.
  
  [github.com/clhenrick](https://github.com/clhenrick/gdal_hillshade_tutorial)
