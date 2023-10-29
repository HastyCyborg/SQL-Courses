# L4: Sub queries & temp tables

- Sub Queries
```
SELECT channel, AVG(no_of_events) AS avg_ev
FROM
(SELECT DATE_TRUNC('day',occurred_at) AS day ,channel,COUNT(*) no_of_events
FROM web_events w
GROUP BY 1,2) AS table1
GROUP BY channel
ORDER BY 2 DESC;
```

- Proper Formatting queries make it easier to understand so use tabs
- Note that you should not include an alias when you write a subquery in a conditional statement. This is because the subquery is treated as an individual value (or set of values in the IN case) rather than as a table
- WITH: Allows us to make tables. Separated by comma.

### --Fin--
