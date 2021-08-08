Nah, no "read" in CRUD, "read" is done by `SELECT` statement and we discussed a lot alread [here](./0-select.md).

## Add new rows

### `INSERT INTO` statement

```sql
/* if you have values of all the columns of a row */
INSERT INTO table_name VALUES (val1, val2, val3, ...)

/* if you only have values of some columns */
INSERT INTO table_name (col1, col2) VALUES (val1, val2)

/* you can also use nested query in the `INSERT` */
INSERT INTO table_name SELECT col1 FROM another_table WHERE col2 > 1;

/* there's some very complicated queries you can use,
below is a query involves 3 tables, which CROSS JOIN tableB, tableC & the max value of col1 of tableC
*/
INSERT INTO tabelA SELECT b.id FROM tableB AS b, tableC AS c, (SELECT MAX(col1) AS max FROM tableC) WHERE c.col1 = max AND b.id = c.id;
```



## Update values

### `UPDATE` statement

```sql
/* update a certain column for all rows in a table */
UPDATE table_name SET col = col * 1.1;

/* update only the rows that meet a criteria */
UPDATE table_name SET col = col * 1.1 WHERE col2 = 'promoted';

/* set multiple columns*/
UPDATE table_name SET col1 = col2, col2 = col1 WHERE <cond>;
```



## Delete values

### `DELETE` statement

```sql
/* just as rm-rf, pay attention to make sure you add a `WHERE` clause when using `DELETE` */
DELETE FROM table_name WHERE id = 1;
```



As `DELETE` is really dangerous, most SQL engines have some thing for you to go back to the previous point. We called it a **transaction**

```sql
BEGIN; /*The beginning of a transaction*/
DELETE FROM table_name;

/* to end a transaction, we have 3 options : */
ROLLBACK; /*undo the delete and complete the transaction*/
COMMIT; /*commit the changes and complete the transaction*/
END; /*also commit the changes and complete the transaction*/

```

