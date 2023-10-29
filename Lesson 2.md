# L2: SQL JOINS 

- JOIN
- ON: 
    We use `ON` clause to specify a `JOIN` condition which is a
    logical statement to combine the table in `FROM` and `JOIN` statements.
- AND
- OR
- We can join as many tables we want and the connection of PK to FK is not one way.

```sql
SELECT *
FROM web_events
JOIN accounts
ON web_events.account_id = accounts.id
JOIN orders
ON accounts.id = orders.account_id
```


- Specifying Aliases: We can specify aliases by writing alias after col name separated by a blank space
- We can also alias column names in such way by writing the alias name after space in `SELECT` part
- It is somewhat replacement of `AS`



## Few QnA's:
![image](https://github.com/HastyCyborg/SQL-Courses/assets/75210542/a2bba08a-572b-4997-8465-f80ee3df9a49)

1. 
```sql
SELECT a.primary_poc, w.occurred_at, w.channel, a.name
FROM web_events w
JOIN accounts a
ON w.account_id = a.id
WHERE a.name = 'Walmart';
```
2.
```sql
SELECT r.name region, s.name rep, a.name account
FROM sales_reps s
JOIN region r
ON s.region_id = r.id
JOIN accounts a
ON a.sales_rep_id = s.id
ORDER BY a.name;
```
3.
```sql
SELECT r.name region, a.name account, 
       o.total_amt_usd/(o.total + 0.01) unit_price
FROM region r
JOIN sales_reps s
ON s.region_id = r.id
JOIN accounts a
ON a.sales_rep_id = s.id
JOIN orders o
ON o.account_id = a.id;
```

```diff
! If you have two or more columns in your SELECT
! that have the same name after the table name such as
! accounts.name and sales_reps.name you will need to alias them.
! Otherwise it will only show one of the columns.
+ You can alias them like:
```
```sql
accounts.name AS AcountName, sales_rep.name AS SalesRepName
```



- LEFT JOINT and RIGHT JOINT Right keyword is not written most of the times rather the FROM and JOIN tables are interchanged depending if RIGHT joint is needed.
These are outer joints
- SELECT DISTINCT a.name, w.channel 
Will allow only distinct values to be displayed on output


### Recap
Choosing the setup of data in our database is very important, but not usually the job of a data analyst. This process is known as Database Normalization.
1. JOIN - an INNER JOIN that only pulls data that exists in both tables.
2. LEFT JOIN - pulls all the data that exists in both tables, as well as all of the rows from the table in the FROM even if they do not exist in the JOIN statement.
3. RIGHT JOIN - pulls all the data that exists in both tables, as well as all of the rows from the table in the JOIN even if they do not exist in the FROM statement.
