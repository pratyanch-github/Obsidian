`OFFSET` is a clause used in SQL queries to skip a specified number of rows before returning the remaining rows. It is often used in conjunction with the `LIMIT` clause to implement pagination or to skip a certain number of top rows. 

For example, if you have a table `employees` and you want to fetch the third and fourth highest-paid employees, you can use `OFFSET` with `LIMIT`:

```sql
SELECT * FROM employees
ORDER BY salary DESC
LIMIT 2 OFFSET 2;
```

In this query, `LIMIT 2` specifies that we want to fetch 2 rows, and `OFFSET 2` specifies that we want to skip the first 2 rows. So, effectively, this query fetches the third and fourth highest-paid employees.