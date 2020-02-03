---
tags: [Notebooks/Postgres and postgis]
title: Dates
created: '2020-02-03T10:39:45.622Z'
modified: '2020-02-03T10:45:22.241Z'
---

# Dates

### Extract data from date - exmaples

```sql
SELECT date::date,
	   extract('isodow' from date) as dow,
	   to_char(date, 'dy') as day,
	   extract('isoyear' from date) as "iso year",
	   extract('week' from date) as week,
	   extract('day' from (date + interval '2 month - 1 day')) as feb,
	   extract('year' from date) as year, 
	   extract('day' from (date + interval '2 month - 1 day')) = 29 as leap
FROM generate_series(date '2000-01-01', date '2010-01-01', interval '1 year')
AS t(date);
```
will give you:

```
date        │ dow │ day │ iso year │ week │ feb │year  │ leap
════════════╪═════╪═════╪══════════╪══════╪═════╪══════╪══════
2000-01-01  │ 6   │ sat │ 1999     │ 52   │ 29 │ 2000  │ t
2001-01-01  │ 1   │ mon │ 2001     │ 1    │ 28 │ 2001  │ f
2002-01-01  │ 2   │ tue │ 2002     │ 1    │ 28 │ 2002  │ f
2003-01-01  │ 3   │ wed │ 2003     │ 1    │ 28 │ 2003  │ f
2004-01-01  │ 4   │ thu │ 2004     │ 1    │ 29 │ 2004  │ t
2005-01-01  │ 6   │ sat │ 2004     │ 53   │ 28 │ 2005  │ f
2006-01-01  │ 7   │ sun │ 2005     │ 52   │ 28 │ 2006  │ f
2007-01-01  │ 1   │ mon │ 2007     │ 1    │ 28 │ 2007  │ f
2008-01-01  │ 2   │ tue │ 2008     │ 1    │ 29 │ 2008  │ t
2009-01-01  │ 4   │ thu │ 2009     │ 1    │ 28 │ 2009  │ f
2010-01-01  │ 5   │ fri │ 2009     │ 53   │ 28 │ 2010  │ f
```

*Source: Art Of Postgresql,  Dimitri Fontaine, chpater 4 Page 99.*


