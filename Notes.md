# Lesson 1: Basic SQL

### Entity Relationship Diagrams

![image](https://github.com/HastyCyborg/SQL-Courses/assets/75210542/0c762ba3-b61d-485c-92bf-7de7b573c904)

- Databases and their qualities.
  Each col in database can contain only similar kind of data to make it fast
- We’ll use Postgress.
- Statements
  - CREATE, DROP, SELECT (it’s for query)
- LIMIT: Using limit to limit the number of rows(entries) to be displayed. Eg. LIMIT 15
- SQL is not case sensitive

Description of using different text editor is given at Lec1 Con. 16.

Code looks now like:
```sql
SELECT occurred_at, account_id, channel
FROM web_events
LIMIT 15;
```

- Order by allows to sort
- We can sort based on multiple values… like:
  - ORDER BY total_amt DESC,account_id
- DESC reverses it to descending order
- WHERE
- During filtering using where we need to keep non numeric data in single quotes like:
  - WHERE name = ‘Exonn Mobil’

Derived columns…
- ALTER : can be used to modify columns, limitations: 1)Cant change name of table or column 2)Cant drop a column 3)Cant decrease size of column if data exists in it.
- RENAME: to rename a table: RENAME emp TO emp1;

```sql
SELECT id, (standard_amt_usd/total_amt_usd)*100 AS std_percent, total_amt_usd
FROM orders
LIMIT 10;
```
