## We work with multiple tables in a database

Every table will have a column ( or collection of columns ) as a unique identifier. We call it `PRIMARY KEY`

To be able to join other tables when querying, we also need to have a `FOREIGN KEY`, which corresponds the `PRIMARY KEY` of other tables we want to join.

### `CROSS JOIN`

This is also confusingly called *no join*, and it's actually a type of `INNER JOIN`.

```sql
SELECT a.name, b.name FROM tableA AS a CROSS JOIN tableB as b;

/* and you can just replace the "CROSS JOIN" by a comma "," */
SELECT a.name, b.name FROM tableA as a, tableB as b;
```



### `INNER JOIN`

If we use tableA as parent table, and tableB as the child table,

Then we'll join `ON` the `PRIMARY` key of tableA, with `FOREIGN` key of tableB, which insist that the col value should exists in **BOTH** tables.

```sql
/* if there's no matching connection between those 2 tables, we'll get nothing */
SELECT * FROM tableA INNER JOIN tableB ON tableA.col1 = tableB.col2

/* or if you only want one col form tableA */
SELECT tableA.col1 FROM tableA INNER JOIN tableB ON tableA.col1 = tableB.col2;
```



### `LEFT JOIN`

This is also see as an *outer join*. It will includes all rows from the first table, even with no match in the second table

```sql
/* if tableB doesn't have some values of col2, then we'll see the output value as `NULL` */
SELECT * FROM tableA LEFT JOIN tableB ON tabelA.col1 = tableB.col2
```



### Multiple `INNER JOIN`s

Sometimes if we don't an 1-1 or 1-many relationships between 2 tables ( so basically they have a many-to-many relationship ), we'll have another "link" table to store the relations between those 2.

```sql
/* assume we have a tableA, a tableB, and an link_table*/
SELECT tableA.col1, tableB.col2 FROM tableA INNER JOIN link_table ON tabelA.col1 = link_table.col1 INNER JOIN tableB ON link_table.col2 = tableB.col2
```



### `UNION JOIN`

You can have 2 tables that hold same column with different values, the `UNION` will return a union (并集) of those 2 tables.

The column must have **same datatype** in both table. If we want to select multiple columns, we must specify them in the **same order**.

- `UNION` ( **remove duplicates** if there's any. )

```sql
SELECT col1, col2 FROM tableA UNION SELECT col1, col2 FROM tableB
```

- `UNION ALL` (won't remove the duplicates)

```sql
SELECT col1 FROM tableA UNION ALL SELECT col1 FROM tableB
```



### Table alias

Imagine you need to type a lot of the same table name again & again

```sql
SELECT * FROM tableA INNER JOIN table_link ON tableA.col1 = table_link.col2 INNER JOIN tableB ON table_link.col3 = tableB.col4;
```

We can use **table alias** to rewrite the above as

```sql
SELECT * FROM tableA AS a INNER JOIN table_link as link ON a.col1 = link.col2 INNER JOIN tableB as b ON link.col3 = b.col4;
```



### Column alias

Same as table alias, we can use `AS` to rename the columns if needed

```sql
SELECT long_col_name_1 AS name1, long_col_name_2 AS name2 FROM tableA
```



### Self `JOIN`

Sometimes one table can contain self referencing data. Think about a table of students that has a classMate field, which reference to some people in the same table.

We can use self `INNER JOIN` to get the data we want.

Heros

| id   | name          | partner_id |
| ---- | ------------- | ---------- |
| 1    | Iron Man      | 2          |
| 2    | Pepper Potts  | 1          |
| 3    | Scarlet Witch | 4          |
| 4    | Vision        | 3          |
| 5    | Ant Man       | 6          |
| 6    | The Wasp      | 5          |

If we want to output two columns called 'character_name' and 'partner_name', we can use `INNER JOIN` of the same table

```sql
SELECT a.name AS character_name, b.name AS partner_name FROM Heros as a INNER JOIN Heros as b ON a.partner_id = b.id;
```

The out put would be:

| character_name | partner_name  |
| -------------- | ------------- |
| Iron Man       | Pepper Potts  |
| Pepper Potts   | Iron Man      |
| Scarlet Witch  | Vision        |
| Vision         | Scarlet Witch |
| Ant Man        | The Wasp      |
| The Wasp       | Ant Man       |

