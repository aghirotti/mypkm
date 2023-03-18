---
alias: Postgres unused cols
---
#postgres #pg_unused_cols


PostgreSQL doesn’t support marking table columns as _unused_. However, when running the `ALTER TABLE… DROP COLUMN` command, the drop column statement doesn’t physically remove the column; it only makes it invisible to SQL operations. As such, dropping a column is a fast action, but doesn’t reduce the ondisk size of your table immediately because the space occupied by the dropped column isn’t reclaimed.

The unused space is reclaimed by new DML actions, as they use the space that once was occupied by the dropped column. To force an immediate reclamation of storage space, use the `VACUUM FULL` command. Alternatively, run an `ALTER TABLE` statement to force a rewrite.

**Examples**

PostgreSQL `drop column` statement.

```sql
ALTER TABLE EMPLOYEES DROP COLUMN COMMISSION_PCT;
```

Verify the operation.

```sql
SELECT TABLE_NAME, COLUMN_NAME
  FROM INFORMATION_SCHEMA.COLUMNS
  WHERE TABLE_NAME = 'emps1' AND COLUMN_NAME=LOWER('COMMISSION_PCT');

table_name  column_name
(0 rows)
```

Use the `VACUUM FULL` command to reclaim unused space from storage.

```sql
VACUUM FULL EMPLOYEES;
```

Run the `VACUUM FULL` statement with the `VERBOSE` option to display an activity report of the vacuum process that includes the tables vacuumed and the time taken to perform the vacuum operation.

```sql
VACUUM FULL VERBOSE EMPLOYEES;
```

For more information, see [ALTER TABLE](https://www.postgresql.org/docs/10/sql-altertable.html)  and [VACUUM](https://www.postgresql.org/docs/13/sql-vacuum.html) in the _PostgreSQL documentation_.