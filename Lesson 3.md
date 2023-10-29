# L3: SQL Aggregations

- NULL: We use IS with NULL during WHERE or any other clause and not (=) because SQL considers NULL as property of data rather than value
NULLs can occur if data is missing

- COUNT:
```sql
SELECT COUNT(*)
FROM accounts;
```

- SUM: will treat NULL values as zero and sum can only be applied to quantitative values


### Question
Find the total amount spent on standard_amt_usd and gloss_amt_usd paper for each order in the orders table. This should give a dollar amount for each order in the table.
```sql
SELECT standard_amt_usd + gloss_amt_usd AS total_standard_gloss
FROM orders;
```
Back to the points...
- MAX and MIN syntactically similar to COUNT, can work on dates or int or strings
- AVG: can be applied only on numerical values and it ignores NULL, don’t include it in either numerator or denominator.
- There is no function for Median

- GROUP BY: The GROUP BY always goes between WHERE and ORDER BY.

- We can only order by the columns using which we group.

- Any column in the SELECT statement that is not within an aggregator must be in the GROUP BY clause

### GROUP BY - Expert Tip
Before we dive deeper into aggregations using GROUP BY statements, it is worth noting that SQL evaluates the aggregations before the LIMIT clause. If you don’t group by any columns, you’ll get a 1-row result—no problem there. If you group by a column with enough unique values that it exceeds the LIMIT number, the aggregates will be calculated, and then some rows will simply be omitted from the results.

This is actually a nice way to do things because you know you’re going to get the correct aggregates. If SQL cuts the table down to 100 rows, then performed the aggregations, your results would be substantially different. The above query’s results exceed 100 rows, so it’s a perfect example. In the next concept, use the SQL environment to try removing the LIMIT and running it again to see what changes.



Again back to the points...
- DISTINCT: provides unique rows for all columns specified, it may slow down queries.
- HAVING: is the “clean” way to filter a query that has been aggregated, but this is also commonly done using a subquery. Essentially, any time you want to perform a WHERE on an element of your query that was created by an aggregate, you need to use HAVING instead.
- HAVING is used when we need to filter data which is based on aggregate functions , WHERE fails in this case

- WHERE subsets the returned data based on a logical condition.
- WHERE appears after the FROM, JOIN, and ON clauses, but before GROUP BY.
- HAVING appears after the GROUP BY clause, but before the ORDER BY clause.
- HAVING is like WHERE, but it works on logical statements involving aggregations.

Some Q/A here during course

- DATE_TRUNC
- DATE_PART
- CASE: Its similar to If statements in other languages. Inside CASE we can write multiple WHEN..THEN..ELSE. statements and finally END.
- The CASE statement always goes in the SELECT clause.


Q/A on case here...
