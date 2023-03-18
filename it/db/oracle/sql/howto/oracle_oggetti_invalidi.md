---
alias: Oggetti invalidi in Oracle
---
#oracle #oracle_sql @oracle_invalid_objs

### Identificare gli oggetti invalidi

```sql
SET LINES           130
COL OWNER       FOR A20
COL OBJECT_NAME FOR A40
COL OBJECT_TYPE FOR A25
COL STATUS      FOR A20

SELECT owner, object_type, object_name, status
  FROM dba_objects
 WHERE status != 'VALID'
ORDER BY owner, object_type;
```



### Compilazione oggetti invalidi

```sql
SET ECHO OFF
SET HEAD OFF
SET FEED OFF
SET VER OFF
SET PAGES 99

SPOOL nome_sql.sql

SELECT owner
     , decode (object_type
              , 'PACKAGE BODY', 'ALTER PACKAGE ' || lower (owner) || '.' || lower (object_name) || ' COMPILE BODY;'
              , 'SYNONYM', (decode (owner
                                   , 'PUBLIC', 'ALTER PUBLIC SYNONYM '|| lower (object_name) ||' COMPILE;'
                                   , 'ALTER ' || object_type || ' ' || lower (owner) || '.' || lower (object_name) || ' COMPILE;'
                                   )
                           )
              , 'ALTER ' || object_type || ' ' || lower (owner) || '.' || lower (object_name) || ' COMPILE;'
              )
  FROM dba_objects
 WHERE STATUS = 'INVALID'
   AND OBJECT_TYPE IN ('PACKAGE BODY', 'PACKAGE', 'FUNCTION', 'PROCEDURE', 'TRIGGER', 'VIEW', 'MATERIALIZED VIEW', 'SYNONYM')
ORDER BY 1, 2; --owner, object_type, object_name;

SPOOL OFF
```

