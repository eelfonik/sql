## The original (statement)

`SELECT * FROM <table>` 

## Be selective (with column names)

`SELECT <col1>, <col2>, <col3> FROM <table>`

## Be specific (with the `WHERE` clause)

`SELECT <col> FROM <table> WHERE <col1>='query'`

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

`SELECT * FROM <table> WHERE <cond1> AND <cond2>`

### Get more ( with `OR` operator)

`SELECT * FROM <table> WHERE <cond1> OR <cond2>`

### Write less for `OR` ( with `IN` operator)

`SELECT * FROM <table> WHERE <col> IN ('query1', 'query2', 'query3')`

### Be exclusive ( with `NOT` operator)

`SELECT * FROM <table> WHERE <col> NOT IN ('query1', 'query2')`

### Fuzzy pattern search ( with `LIKE` operator and wildcard options)

- `%` to unlimited wildcard

  `SELECT * FROM <table> WHERE <col> LIKE '%<query>%'` -> So as we used the `%`, this will return all rows that contains the query string in their <col> in any places.
  If you only want to get rows **starts** or **ends** with that query, you can remove one of the `%` as you want.

- `_` to specific exactly how many wildcard characters

  `SELECT * FROM <table> WHERE <col> LIKE '_____'` -> will return all rows that `col` contains exactly 5 characters 