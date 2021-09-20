---
tags: [Notebooks/Pandas]
title: Pandas Data Cleaning
created: '2020-10-05T07:29:15.002Z'
modified: '2020-10-05T07:34:00.565Z'
---

# Pandas Data Cleaning

### How to remove NaN from df


```python
import pandas as pd

df = pd.read_csv("...")

df.dropna(self, axis=0, how="any", thresh=None, subset=None, inplace=False)
```

* axis: possible values are {0 or ‘index’, 1 or ‘columns’}, default 0. If 0, drop rows with null values. If 1, drop columns with missing values.
* how: possible values are {‘any’, ‘all’}, default ‘any’. If ‘any’, drop the row/column if any of the values is null. If ‘all’, drop the row  column if all the values are missing.
* thresh: an int value to specify the threshold for the drop operation.
* subset: specifies the rows/columns to look for null values.
* inplace: a boolean value. If True, the source DataFrame is changed and None is returned.


*Source: [journaldev.com](https://www.journaldev.com/33492/pandas-dropna-drop-null-na-values-from-dataframe)*
