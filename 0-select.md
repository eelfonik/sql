## The original (`SELECT` statement)

```sql
SELECT * FROM <table>
```

## Be selective (with column names)

```sql
SELECT <col1>, <col2>, <col3> FROM <table>
```

Rename ! : you can give the col's other name with `AS` alias 

```sql
SELECT col1 AS myFancyName FROM table_name
```

Calc ! (you can use the basic operators like `+`, `-`, `*`, `/` , and use `()` )

```sql
SELECT col1, (col2 * 3000 + col3 + 5) AS temp FROM table_name
```



## Be specific (with `WHERE` clause)

```sql
SELECT <col> FROM <table> WHERE <col1>='query'
```

the `=` in the `WHERE` clause is just one of the **comparision operators** you can use, we have lots of them

| Operator | Description                              |
| :------- | ---------------------------------------- |
| =        | Equal to                                 |
| !=       | NOT equal to                             |
| <>       | NOT equal to (???)                       |
| <        | Less than                                |
| <=       | Less than or Euqal to                    |
| >        | Greater than (Only on numeric field ???) |
| >=       | Greater than or Equal to                 |

### Be even more specific ( with `AND` operator)

```sql
SELECT * FROM <table> WHERE <cond1> AND <cond2>
```

### Get more ( with `OR` operator)

```sql
SELECT * FROM <table> WHERE <cond1> OR <cond2>
```

### Write less for `OR` ( with `IN` operator)

```sql
SELECT * FROM <table> WHERE <col> IN ('query1', 'query2', 'query3')
```

### Be exclusive ( with `NOT` operator)

```sql
SELECT * FROM <table> WHERE <col> NOT IN ('query1', 'query2')
```

### Fuzzy pattern search ( with `LIKE` operator and wildcard options)

- `%` to unlimited wildcard

  ```sql
  SELECT * FROM <table> WHERE <col> LIKE '%<query>%'
  ```

  As we used the `%`, this will return all rows that *contains* the query string in their <col> in any places.
  If you only want to get rows **starts** or **ends** with that query, you can remove one of the `%` as you want.

- `_` to specific exactly how many wildcard characters

  ```sql
  SELECT * FROM <table> WHERE <col> LIKE '_____'
  ```
  
  will return all rows that `col` contains exactly 5 characters 

### Handle `NULL`

We can select either `NULL` value or not directly by using the conditions with `WHERE` clause

```sql
/* get all rows that the value of `col` is `NULL`*/
SELECT * FROM table WHERE col IS NULL

/* or filter out the `NULL` value */
SELECT * FROM table WHERE col IS NOT NULL
```



### Dates (devils 😈)

Dates are with different formats. Let's assume we just use the `yyyy-mm-dd` format.

```sql
SELECT name, dob, email FROM <table> WHERE dob < '2000-01-01'
```

### Nested queries

The conditions applied to the `WHERE` clause can itself be a query ( **inner query** ), which is VERY helpful if the value is dynamic !

```sql
SELECT * FROM table WHERE price = (SELECT MIN(price) FROM table);
```

### Results of a query can be queried as a real table 💥💥💥💥💥💥💥💥

It can be nested quite deep.... One thing in SQL is, **the results of a query can be queried as a real table** !!!!

```sql
SELECT COUNT(*) FROM tableA, (SELECT AVG(price) AS ap1 FROM tableA, (SELECT AVG(price) AS ap FROM tableA) WHERE price > ap) WHERE price > ap1;

/* let's break it down:
1. The `(SELECT AVG(price) AS ap FROM tableA)`, where we get the average price of all the table rows. We mark it as `inner_table` that contains only one record, an avg number (ap).
2. Then `(SELECT AVG(price) AS ap1 FROM tableA, (SELECT AVG(price) AS ap FROM tableA) WHERE price > ap)`
is treated as `(SELECT AVG(price) AS ap1 FROM tableA, inner_table WHERE price > inner_table.ap)`, so we get the avg price of all rows that have a price higher than the avg price of all rows in the table, which virtually become another `inner_table2`, than contains only on record (ap1).
3. Then the query become `SELECT COUNT(*) FROM tableA, inner_table2 WHERE price > inner_table2.ap1`, So we get the count of rows that have higher price than average price (ap1) of only the rows that have higher than average price (ap)
*/

```



## Be unique ( with `DISTINCT` keyword)

```sql
SELECT DISTINCT <col> FROM <table>
```

so if we have duplicates in the col, we'll only get a list of **distinct** values.

## Be organized ( with `ORDER BY` keyword)

- from lowest to heighest

```sql
SELECT <col> FROM <table> ORDER BY <col1>
```

- Or do it revese with `DESC`, from heighest to lowest:

```sql
SELECT <col> FROM <table> ORDER BY <col1> DESC
```

- specify multiple cols in `ORDER BY`, so if the first col's values are the same for multiple rows, they'll be sort by the second col

```sql
SELECT * FROM table ORDER BY col1 DESC, col2
```



## Be flexible ( with `CASE` statement )

As it's a statement, so you need to separate it with `,` from `SELECT`.

```sql
SELECT EmployeeName,
CASE
    WHEN EmpLevel = 1 THEN 'Data Scientist'
    WHEN EmpLevel = 2 THEN 'Middle Manager'
    WHEN EmpLevel = 3 THEN 'Industry Visionary'
    ELSE 'Unemployed'
END 
FROM Employees;
```

The default `ELSE` will return `NULL` if you omit it.

TODO: what `THEN` means in this query ?

## Take just a slice (with `LIMIT` clause)

```sql
SELECT * FROM table WHERE id>100 ORDER BY id LIMIT 1
```

( mySQL use another flavor with `SELECT TOP` statement )

It's useful when you only want to get a taste of the data, or, actually you can use it together with `ORDER BY` to get the most whatever row

```sql
SELECT * FROM table ORDER BY height LIMIT 1 
/*get the shortest one from the table*/
/* 😅 normally you'll do it use the `MIN()` or `MAX()` function */
SELECT MIN(height) FROM table
```

## See segment ! ( with `GROUP BY` clause )

```sql
/* will display the results with total count of `col2`, seperatly by `col1` */
SELECT col1, COUNT(col2) FROM table GROUP BY col1
```

This can be handy when using together with the `JOIN`s

```sql
SELECT tableA.col1, COUNT(tableB.col2) AS b_count FROM tableA LEFT JOIN tableB ON tableA.id = tableB.b_id GROUP BY tableA.col1
```



## Operate on aggregated data again (with `HAVING` clause)

The standard SQL is runnig in the following order:

1. `FROM` & `JOIN`s, to know which data set to operate on
2. `WHERE` clause that filters out the data with a given criteria.
3. `GROUP BY` or `ORDER BY`  or the above **aggregate functions** ( like `COUNT` ) to get aggregated data

Then if we want to further operate on the aggregated data, we're running out.

So we have `HAVING` for rescue, it acts like `WHERE` clause, just it can be applied after gouping ( aggregation )

```sql
/* show col with count, group by col, and the count is greater than 1 */
SELECT col, COUNT(*) FROM table GROUP BY col HAVING COUNT(*) > 1
```

