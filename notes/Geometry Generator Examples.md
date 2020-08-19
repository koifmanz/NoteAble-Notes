---
tags: [Notebooks/qgis]
title: Geometry Generator Examples
created: '2019-12-08T10:47:33.425Z'
modified: '2020-08-19T06:37:57.858Z'
---

# Geometry Generator Examples

### Create Minimal circle

use the following code in geom gen
```python
if(
  area($geometry)/area(minimal_circle($geometry, 100))>0.67,
  minimal_circle($geometry, 100)
  null
)
```

<p align="center">
  <img src="https://pbs.twimg.com/media/ER86y_tWoAIQV21?format=jpg&name=medium" width="700">
</p>

*Source: [Twitter: @klaskarlsson](https://twitter.com/klaskarlsson/status/1233769749240336385/photo/1)*

### Links

* [stuyts.xyz](https://stuyts.xyz/2018/11/05/qgis-geometry-generator-examples-repository/ "QGIS Geometry Generator examples repository")
* [polemic.nz](https://polemic.nz/2019/11/18/foss4g-qgis-geometry-generators/ "FOSS4G / QGIS Geometry Generators")


