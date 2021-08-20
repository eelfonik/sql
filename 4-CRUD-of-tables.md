Again, no "read" in CRUD, "read" is done by table joining and we discussed a lot alread [here](./2-joining-tables.md).

## Create a table

```sql
/* just seperate the cols you want to have in the table with comas (,)*/
CREATE TABLE tablename (columnname datatype constraints, ...)

/* Or you can use the same way as create a view, just this time it will be a real table with the data at the time when it's created */
CREATE TABLE tablename AS somequery

/* Examples*/

CREATE TABLE persons (personid INTEGER PRIMARY KEY, name TEXT, hats INTEGER)
/* Populate data to the newly created table */
INSERT INTO persons (name, hats) VALUES ('John', 3);
INSERT INTO persons (name, hats) VALUES ('Mary', 2);

```



### datatype

Most db engine have the following data types:

- `CHAR(length)`
- `VARCHAR(length)`
- `NUMERIC(length.decimals)`
- `INTERGER`
- `REAL` ( what's that ??? )
- `FLOAT(length)`
- `DOUBLE`
- `DATE`
- `TIME`
- `MONEY`
- `BLOB`

It's varied from one db engine to another

### constraints

This is the third item you can put when creating a table with columns, to limit the colum a bit when you **insert data**.

Some of them:

- `PRIMARY KEY` : as it's the identifier of the row, normally the value should be unique, and cannot be null
- `UNIQUE`
- ` NOT NULL`
- `FOREIGN KEY` : the value of this column MUST can be found in other tables' `PRIMARY KEY`, otherwise it will error out
- `CHECK` : this one is kind of like a query, you can say `CHECK(sum<100)` to make sure that the value inserted is within a certain range.



## Delete table

```sql
DROP TABLE tablename
```



## Alter table

There's some altertations you can do to a table that's already in use. Which also varies from one db engine to another

Though maybe it's safer to create new table and move the data from the old table to the new one.

- `RENAME TO` : `ALTER TABLE tableA RENAME TO tableB`
- `ADD COLUMN`: `ALTER TABLE tableA ADD COLUMN colname datatype constraints` -> here N.B. that you cannot add a `NOT NULL` constraint, because the new column will be filled with `NULL` when added.
- `DROP COLUMN` : `ALTER TABLE tableA DROP COLUMN colname`
- `RENAME COLUMN ... TO ...`: `ALTER TABLE tableA RENAME COLUMN colname TO anothercolname`
- `MODIFY COLUMN`: `ALTER TABEL tabelA MODIFY COLUMN colname CHAR(200) NOT NULL` -> this one is specific to change the datatype of a column ( SO what happened if the values already inside the column are not conform to the new datatype ????? N.B. some db engines won't have this )

