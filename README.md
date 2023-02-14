# SQL-Practice (Data Lemur)

# 1 Data Science Skills (LinkedIn SQL Interview Question)
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

# 2 Page With No Likes (Facebook SQL Interview Question)
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

Solution #2: Using NOT EXISTS
```sql
SELECT page_id
FROM pages
WHERE NOT EXISTS (
  SELECT 1
  FROM page_likes AS likes
  WHERE likes.page_id = pages.page_id);
```
  
Solution #3: Using EXCEPT
```sql
SELECT page_id
FROM pages
EXCEPT
SELECT page_id
FROM page_likes
ORDER BY page_id;
```

# 3 Unfinished Parts [Tesla SQL Interview Question]

Tesla is investigating bottlenecks in their production, and they need your help to extract the relevant data. Write a query that determines which parts have begun the assembly process but are not yet finished.

Assumptions

- Table parts_assembly contains all parts in production.
- A part with no finish_date is an unfinished part.

```parts_assembly``` Table:
| Column Name	| Type |
| ----------- | ----------- |
| part |	string |
| finish_date	| datetime |
| assembly_step	| integer |

```sql
SELECT DISTINCT part 
FROM parts_assembly
WHERE finish_date is NULL;
```
