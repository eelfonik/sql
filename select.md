## The original (`SELECT` statement)

```sql
SELECT * FROM <table>
```

## Be selective (with column names)

```sql
SELECT <col1>, <col2>, <col3> FROM <table>
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

### Dates (devils 😈)

Dates are with different formats. Let's assume we just use the `yyyy-mm-dd` format.

```sql
SELECT name, dob, email FROM <table> WHERE dob < '2000-01-01'
```



## Be unique ( with `DISTINCT` keyword)

```sql
SELECT DISTINCT <col> FROM <table>
```

so if we have duplicates in the col, we'll only get a list of **distinct** values.

## Be organized ( with `ORDER BY` keyword)

```sql
SELECT <col> FROM <table> ORDER BY <col1>
```

from lowest to heighest

Or do it revese with `DESC`:

```sql
SELECT <col> FROM <table> ORDER BY <col1> DESC
```

 from heighest to lowest

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

