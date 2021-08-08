## `COUNT()`

Get the total number of a search result

```sql
SELECT COUNT(*) FROM table WHERE <cond>
```

You can drop the `WHERE` clause if you want to count the whole table.

## `SUM()`

You can sumup a specific column (so no wildcard here)

```sql
SELECT SUM(col) FROM table
```



## `AVG()`

It's actaully the **mean** of the data

```sql
SELECT AVG(col) FROM table
```



## `MIN()` & `MAX()`

```sql
SELECT MIN(col), MAX(col) FROM table
```



## `COALESCE()` to treat `NULL` value with a default value

```sql
SELECT col1+col2+COALESCE(NULL, 0) FROM table

/* if the col1/col2 yield `NULL`, we use `0` in the sum */
SELECT SUM(COALESCE(col1/col2, 0)) FROM table

/* we can also use this to specify an order of preference.
The following example will try to get first the `phone1`, if it's `NULL`, then go to get the next one
*/
SELECT name, COALESCE(phone1, phone2, phone3) as phone FROM table
```


