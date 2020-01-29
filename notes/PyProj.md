---
tags: [Notebooks/GDAL]
title: PyProj
created: '2019-12-08T10:41:03.218Z'
modified: '2019-12-09T09:23:11.430Z'
---

# PyProj

### PyProj install failed
Download and install VS 14.0+ [build tools](https://kenboxit.wordpress.com/2018/01/15/python-installing-pyproj-via-pip-on-windows-failed-with-error-code-1).

### PyProj Convert to ITM (or other projections) In Python
```python
def reproject_wgs_to_itm(longitude, latitude):
    prj_wgs = Proj(init='epsg:4326') # Current Projection
    prj_itm = Proj(init='epsg:2039') # Target Projection
    x, y = transform(prj_wgs, prj_itm, longitude, latitude)
    return x, y
```
