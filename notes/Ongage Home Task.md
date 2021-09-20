---
tags: [Notebooks/Interview-Tasks]
title: Ongage Home Task
created: '2021-07-05T10:23:49.912Z'
modified: '2021-07-05T11:44:27.326Z'
---

# Ongage Home Task

# Table of contents
1. [Introduction](#introduction)
2. [Question 1](#Q1)
    1. [Method 1](#Q1-1)
    2. [Method 2 1.2](#Q1-2)
3. [Question 2](#Q2)

## Introduction <a name="introduction"></a>

Introduction

## Q-1 <a name="Q1"></a>

For method 1 I used windows function to rank by likes based on the questions ids.  For the second method I created groups based on the ids and return the max number of likes. After that I used joins to retrieve the answer and questions texts.

### Method 1 <a name="Q1-1"></a>

```SQL
with likes_pos as (
-- rank likes by q text\id and by order of likes
select
	q_text,
	likes,
	answer_text,
	rank() over (partition by q_text
order by
	likes desc) as like_rank
from
	ongage.q1_1 as q_table
join ongage.q1_2 as a_table on
	a_table.q_id = q_table.id)
-- select only the first rank
 select
	q_text,
	answer_text
from
	likes_pos
where
	like_rank = 1
```

### Method 2 <a name="Q1-2"></a>

```SQL

-- method 2
 with likes_max_cte as (
-- get answers with max likes
select
	q_id,
	max(likes) as max_likes
from
	ongage.q1_2 as a_table
group by
	q_id),
cte_join_q as (
-- join q text
select
	q_text,
	q_id,
	max_likes
from
	likes_max_cte
join ongage.q1_1 as q_table on
	likes_max_cte.q_id = q_table.id)
-- Join answers to q text
 select
	q_text,
	answer_text
from
	cte_join_q
inner join ongage.q1_2 as tbl_answers on
	cte_join_q.max_likes = tbl_answers.likes
```

## Q-2 <a name="Q2"></a>

I caluclte ctr for each requested type using case and group by. The get all the results on one table I used join.


```SQL
-- table for total ctr per email
 with cte_total as (
select
	email,
	ROUND(SUM(case when event_name = 'click' then 1 else 0 end) / SUM(case when event_name = 'delivery' then 1 else 0 end)::numeric, 2) as ctr_total
from
	ongage.q2 as events_tbl
group by
	email),
-- table for total ctr per email and message
 cte_messages as (
select
	email,
	message,
	ROUND(SUM(case when event_name = 'click' then 1 else 0 end) / SUM(case when event_name = 'delivery' then 1 else 0 end)::numeric, 2) as ctr_message
from
	ongage.q2 as events_tbl
group by
	email,
	message)
-- join the results
 select
	cte_messages.email as email,
	ctr_total,
	message,
	ctr_message
from
	cte_total
join cte_messages on
	cte_total.email = cte_messages.email
```
