Lesson 2, Lec 19:

## Questions

1. Provide a table that provides the __region__ for each **sales_rep** along with their associated **accounts**. This time only for the Midwest region. Your final table should include three columns: the region name, the sales rep name, and the account name. Sort the accounts alphabetically (A-Z) according to account name.


2. Provide a table that provides the **region** for each **sales_rep** along with their associated **accounts**. This time only for accounts where the sales rep has a first name starting with S and in the Midwest region. Your final table should include three columns: the region name, the sales rep name, and the account name. Sort the accounts alphabetically (A-Z) according to account name.


3. Provide a table that provides the **region** for each **sales_rep** along with their associated **accounts**. This time only for accounts where the sales rep has a last name starting with K and in the Midwest region. Your final table should include three columns: the region name, the sales rep name, and the account name. Sort the accounts alphabetically (A-Z) according to account name.


4. Provide the **name** for each region for every **order**, as well as the account **name** and the **unit price** they paid (total_amt_usd/total) for the order. However, you should only provide the results if the **standard order quantity** exceeds 100. Your final table should have 3 columns: **region name, account name, and unit price**. In order to avoid a division by zero error, adding .01 to the denominator here is helpful total_amt_usd/(total+0.01).


5. Provide the **name** for each region for every **order**, as well as the account **name** and the **unit price** they paid (total_amt_usd/total) for the order. However, you should only provide the results if the **standard order quantity** exceeds 100 and the **poster order quantity** exceeds 50. Your final table should have 3 columns: region name, account name, and unit price. Sort for the smallest unit price first. In order to avoid a division by zero error, adding .01 to the denominator here is helpful (total_amt_usd/(total+0.01).


6. Provide the name for each region for every order, as well as the account name and the unit price they paid (total_amt_usd/total) for the order. However, you should only provide the results if the **standard order quantity exceeds** 100 and the **poster order quantity** exceeds 50. Your final table should have 3 columns: region name, account name, and unit price. Sort for the largest unit price first. In order to avoid a division by zero error, adding .01 to the denominator here is helpful (total_amt_usd/(total+0.01).


7. What are the different channels used by account id 1001? Your final table should have only 2 columns: **account name** and the different **channels**. You can try `SELECT DISTINCT` to narrow down the results to only the unique values.


8. Find all the orders that occurred in 2015. Your final table should have 4 columns: **occurred_at, account name, order total,** and **order total_amt_usd**.


## Solutions

1.
```sql
SELECT r.name AS RegName, s.name AS SalesRName,
a.name AS AccName
FROM sales_reps s
JOIN accounts a
ON a.sales_rep_id=s.id
JOIN region r
ON s.region_id=r.id AND
r.name='Midwest'
ORDER BY a.name;
```

2.
```sql
SELECT r.name AS RegName, s.name AS SalesRName,
a.name AS AccName
FROM sales_reps s
JOIN accounts a
ON a.sales_rep_id=s.id
JOIN region r
ON s.region_id=r.id AND
r.name='Midwest'
WHERE s.name LIKE 'S%'
ORDER BY a.name;
```

3.
```sql
 SELECT r.name AS RegName, s.name AS SalesRName,
a.name AS AccName
FROM sales_reps s
JOIN accounts a
ON a.sales_rep_id=s.id
JOIN region r
ON s.region_id=r.id AND
r.name='Midwest'
WHERE s.name LIKE '% K%'
ORDER BY a.name;
```

4.
```sql
SELECT r.name AS RegName, (o.total_amt_usd/(o.total+0.01)) AS UnitPr,
a.name AS AccName
FROM sales_reps s
JOIN accounts a                               
ON a.sales_rep_id=s.id
JOIN region r
ON s.region_id=r.id
JOIN orders o
ON o.account_id=a.id AND o.standard_qty>100
```

5.
```sql
SELECT r.name AS RegName, (o.total_amt_usd/(o.total+0.01)) AS UnitPr,
a.name AS AccName
FROM sales_reps s
JOIN accounts a                               
ON a.sales_rep_id=s.id
JOIN region r
ON s.region_id=r.id
JOIN orders o
ON o.account_id=a.id AND o.standard_qty>100 AND poster_qty>50
ORDER BY UnitPr;
```

6.
```sql
SELECT r.name AS RegName, (o.total_amt_usd/(o.total+0.01)) AS UnitPr,
a.name AS AccName
FROM sales_reps s
JOIN accounts a                               
ON a.sales_rep_id=s.id
JOIN region r
ON s.region_id=r.id
JOIN orders o
ON o.account_id=a.id AND o.standard_qty>100 AND poster_qty>50
ORDER BY UnitPr DESC;
```

7.
```sql
SELECT DISTINCT a.name acc_name, w.channel
FROM accounts a
JOIN web_events w
ON w.account_id=a.id
WHERE a.id=1001
```

8.
```sql
SELECT a.name AS "account name", o.occurred_at,o.total,o.total_amt_usd
FROM orders o
JOIN accounts a
ON a.id=o.account_id
WHERE occurred_at BETWEEN '2015-01-01' AND '2016-01-01'
ORDER BY o.occurred_at DESC;

```
