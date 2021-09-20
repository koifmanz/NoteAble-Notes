---
tags: [Notebooks/Interview-Tasks]
title: Data Engineer / Analys Task - Verizon Media
created: '2021-07-01T12:48:48.962Z'
modified: '2021-07-02T05:41:47.362Z'
---

# Data Engineer / Analys Task -  Verizon Media

# Table of contents
1. [Introduction](#introduction)
2. [Question 1](#Q1)
    1. [Question 1.1](#Q1-1)
    2. [Question 1.2](#Q1-2)
3. [Question 2](#Q2)
4. [Question 3](#Q3)

## Introduction <a name="introduction"></a>

I alterd the strings in *datestamp* into date type. I assumed that I will recive the date for the query as a string, which mean I will need to convert it into date type also.

```SQL
ALTER TABLE daily_pre_agg ADD COLUMN spend_date DATE;

UPDATE
    daily_pre_agg
SET
    spend_date = TO_DATE(datestamp, 'YYYYMMDD');
```

## Q-1 <a name="Q1"></a>

I sum the *spend* column using group by and filter with the *date* column created earlier.

### Q-1.1 <a name="Q1-1"></a>

```SQL
SELECT
    account_id,
    SUM(spend) as total_spend
FROM
    daily_pre_agg
WHERE
    spend_date = TO_DATE('20200316', 'YYYYMMDD')
GROUP BY
    account_id
ORDER BY
    total_spend desc
LIMIT 5;
```

### Q-1.2 <a name="Q1-2"></a>

```SQL
SELECT
    account_id,
    sum(spend) as total_spend
FROM
    daily_pre_agg
WHERE
    spend_date BETWEEN TO_DATE('20200316', 'YYYYMMDD') AND TO_DATE('20200322', 'YYYYMMDD')
GROUP BY
    account_id
ORDER BY
    total_spend desc
LIMIT 5;
```

## Q-2 <a name="Q2"></a>

I used the following steps: 
  1. UNION - create list including all the accounts. In cte table
  2. Two cte tables of spending, one for each date.
  3. Left Join - to add the spending from each date, and keep the account ids without spending.
  4. SELECT the the requested results (*diff_in_spend* column)


```SQL
WITH cte_ids as(
-- create list of all the ids
SELECT
    account_id
FROM
    daily_pre_agg
WHERE
    spend_date = TO_DATE('20170313', 'YYYYMMDD')
GROUP BY
    account_id
UNION
SELECT
    account_id
FROM
    daily_pre_agg
WHERE
    spend_date = TO_DATE('20170320', 'YYYYMMDD')
GROUP BY
    account_id),
cte_0313 as(
-- a table for the spendings in 20200313 by id
SELECT
    account_id ,
    SUM(spend) as spend_0313
FROM
    daily_pre_agg
WHERE
    spend_date = TO_DATE('20170313', 'YYYYMMDD')
GROUP BY
    account_id),
cte_0320 as(
-- a table for the spendings in 20200320 by id
SELECT
    account_id ,
    SUM(spend) as spend_0320
FROM
    daily_pre_agg
WHERE
    spend_date = TO_DATE('20170320', 'YYYYMMDD')
GROUP BY
    account_id)
-- join the data and calculate the the difference 
SELECT
    cte_ids.account_id,
    cte_0313.spend_0313 as spend_0313,
    cte_0320.spend_0320 as spend_0320,
    (cte_0313.spend_0313-cte_0320.spend_0320) as diff_in_spend
FROM
    cte_ids
LEFT JOIN cte_0313 on
    cte_ids.account_id = cte_0313.account_id
LEFT JOIN cte_0320 on
    cte_ids.account_id = cte_0320.account_id;
```

## Q-3 <a name="Q3"></a>

I used case and group by to create the bins, and then calculate the requested data.


```SQL
SELECT
    CASE
        WHEN spend < 100 THEN 'Less then 100$'
        WHEN spend BETWEEN 100 and 1000 THEN 'Between 100$ and 1000$'
        WHEN spend BETWEEN 1001 and 10000 THEN 'Between 1001$ and 10000$'
        WHEN spend > 10000 THEN 'More then 10000$'
    END spend_groups,
    COUNT(distinct (account_id)) as unique_advertisers_amount,
    ROUND((COUNT(DISTINCT (account_id)))/(COUNT(account_id)::numeric)* 100, 2) as advertisers_proportion
FROM
    daily_pre_agg
WHERE
    spend_date = TO_DATE('20200316', 'YYYYMMDD')
GROUP BY
    spend_groups;
```
