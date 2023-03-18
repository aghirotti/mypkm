---
alias: "Colonne non usate in una tabella"
---

#oracle_unused_cols #alter_table #oracle_sql #sql #oracle
Oracle provides a method to mark columns as _unused_. Unused columns aren’t physically dropped, but are treated as if they were dropped. Unused columns can’t be restored. Select statements don’t retrieve data from columns marked as unused and aren’t displayed when running a `DESCRIBE` table command.

The main advantage of setting a column to UNUSED is to reduce possible high database load when dropping a column from a large table. To overcome this issue, a column can be marked as unused and then be physically dropped later.

To set a column as unused, use the `SET UNUSED` clause.

**Examples**

```sql
ALTER TABLE EMPLOYEES SET UNUSED (COMMISSION_PCT);
ALTER TABLE EMPLOYEES SET UNUSED (JOB_ID, COMMISSION_PCT);
```

### Display unused columns.

```sql
SELECT * FROM USER_UNUSED_COL_TABS;

TABLE_NAME  COUNT
EMPLOYEES   3
```

### Drop the column permanently (physically drop the column).

```sql
ALTER TABLE EMPLOYEES DROP UNUSED COLUMNS;
```

For more information, see [CREATE TABLE](https://docs.oracle.com/en/database/oracle/oracle-database/19/sqlrf/CREATE-TABLE.html#GUID-F9CE0CC3-13AE-4744-A43C-EAC7A71AAAB6) in the _Oracle documentation_.