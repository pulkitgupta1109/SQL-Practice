# SQL-Practice (Data Lemur)

# 1 LinkedIn SQL Interview Question
Given a table of candidates and their skills, you're tasked with finding the candidates best suited for an open Data Science job. You want to find candidates who are proficient in Python, Tableau, and PostgreSQL.

Write a query to list the candidates who possess all of the required skills for the job. Sort the output by candidate ID in ascending order.

Assumption: There are no duplicates in the candidates table.


```candidates``` Table:
| Column Name | Type |
| ----------- | ----------- |
| candidate_id | integer |
| skill | varchar |

```sql
SELECT candidate_id 
FROM candidates 
WHERE skill IN ('Python', 'Tableau', 'PostgreSQL')
GROUP BY candidate_id 
HAVING count(skill)=3
ORDER BY candidate_id;

```

# 2 Facebook SQL Interview Question
Assume you are given the tables below about Facebook pages and page likes. Write a query to return the page IDs of all the Facebook pages that don't have any likes. The output should be in ascending order.

``` pages ``` Table:
| Column Name | Type |
| ----------- | ----------- |
| page_id | integer |
| page_name | varchar |

```page_likes``` Table:
| Column Name	| Type |
| ----------- | ----------- |
| user_id	| integer |
| page_id	| integer |
| liked_date | datetime |

```sql
SELECT pg.page_id 
FROM pages pg LEFT JOIN page_likes pgl
ON pg.page_id = pgl.page_id
WHERE pgl.page_id is NULL ;
```


