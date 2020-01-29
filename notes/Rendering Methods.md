---
tags: [Notebooks/Cartography]
title: Rendering Methods
created: '2020-01-21T07:11:31.422Z'
modified: '2020-01-21T13:27:21.840Z'
---

# Rendering Methods


### Resampling

* Nearest Neighbor - great for categorical, because of the blocky results.
* Bilinear - best for continuous data. use in zoom in when creating hillshade. 
* Cubic - great for continuous data.
* Average - great for continuous data. use in zoom out when creating hillshade.

*Source: discover QGIS 3.x, Kurt Menke, chpater 5 Exercice 1, page 336.*


### Blending

* Multiply - Darken group - use to show both layers at full saturation. for example hillshade and land use layer. multiplies the corresponding values of every two pixel for both layers.
* Screen - opposite to multiply (multipliy the light pixels)
* Overlay - Contrast group - combines the multiply and screen methods, so light part are lighter, and dark parts are darker. example: border layer, when less important.

*Sources*: 
1. *discover QGIS 3.x, Kurt Menke, chpater 5 Exercice 1, page 336.*
2. *[Qgis User Manual](https://docs.qgis.org/2.18/en/docs/user_manual/introduction/general_tools.html?highlight=blending#blending-modes) - blending chapter.*


