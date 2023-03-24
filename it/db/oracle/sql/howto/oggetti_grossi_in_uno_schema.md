---
alias: Oggetti di ampie dimensioni in uno schema Oracle
---
#oracle #oracle_sql #oracle_big_objs

### I primi 10 oggetti in ordine di dimensione

```sql
SET LINES 400
COL tablespace_name FORMAT A20
COL partition_name  FORMAT A16
COL owner           FORMAT A15
COL segment_name    FORMAT A32
COL segment_type    FORMAT A15

SELECT tablespace_name, owner, segment_name, segment_type, partition_name, mb
  FROM (
        SELECT tablespace_name
             , owner
             , segment_name
             , segment_type
             , partition_name 
             , bytes / 1024 / 1024  AS MB
          FROM dba_segments
        ORDER BY bytes DESC
       )
 WHERE rownum < 10;
```

