---
tags: [Notebooks/Postgres and postgis]
title: Sorting
created: '2019-12-08T11:48:34.365Z'
modified: '2019-12-08T11:54:24.655Z'
---

# Sorting

### Select top N records for each category

```sql
SELECT rs.Field1,rs.Field2 
    FROM (
        SELECT Field1,Field2, Rank() 
          over (Partition BY Section
                ORDER BY RankCriteria DESC ) AS Rank
        FROM table
        ) rs WHERE Rank <= 10
```

##### References
[StackOverflow](https://stackoverflow.com/questions/176964/select-top-10-records-for-each-category)
[medium](https://medium.com/@amulya349how-to-select-top-n-rows-from-each-category-in-postgresql-39e3cfebb020)


