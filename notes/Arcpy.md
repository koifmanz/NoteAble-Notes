---
tags: [Notebooks/ArcGIS]
title: Arcpy
created: '2019-12-08T11:55:40.190Z'
modified: '2020-01-29T12:25:51.363Z'
---

# Arcpy

### Select By Layer

```
query = """ "ATTRIBUTE_NAME" = '%s'"""%val
arcpy.SelectLayerByAttribute_management("Sample", "NEW_SELECTION", query)
```
