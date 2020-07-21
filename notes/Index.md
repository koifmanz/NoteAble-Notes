---
tags: [Notebooks/Postgres and postgis]
title: Index
created: '2020-07-21T09:58:14.670Z'
modified: '2020-07-21T10:06:59.208Z'
---

# Index

### GIST vs GIN

**GIN** is especially useful for all kinds of full **text operations** while **GIST** is ideal for **geometric data (GIS)**. GIN does not speed up the “=” operator. So if you are looking for a normal lookup you will need a second index.

Also in general GIN is use less space in HD.

1. *Create GIST Index*
```sql
CREATE INDEX idx_gist ON t_hash USING gist (md5 gist_trgm_ops);
```

Schema |   Name   |  Type | Owner |  Table |   Size  | 
--------|----------|-------|-------|--------|---------
 public | idx_gist | index |    hs | t_hash | 8782 MB |

2. *Create GIN Index*
```sql
CREATE INDEX idx_gin ON t_hash USING gin (md5);
```

3. *Create Regular Index*
```sql
CREATE INDEX idx_btree ON t_hash (md5);
```

 Schema |    Name   |  Type | Owner |  Table |    Size |
--------|-----------|-------|-------|--------|---------|
 public | idx_btree | index |    hs | t_hash | 2816 MB | 
 public |  idx_gist | index |    hs | t_hash | 2807 MB |

##### References
[CyberTech: Better Like and Ilike](https://www.cybertec-postgresql.com/en/postgresql-more-performance-for-like-and-ilike-statements/)
