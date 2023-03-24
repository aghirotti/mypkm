---
alias: Privilegi di una tabella
---

#### Trova i privilegi di una tabella

```sql
SELECT a.table_schema AS DB_SCHEMA
     , a.table_name   AS TABELLA
     , a.grantor      AS USER_CHE_HA_DATO_IL_PRIV
     , a.privilege    AS TIPO_GRANT
     , a.grantee      AS USER_CHE_HA_RECEVUTO_IL_PRIV
  FROM all_tab_privs a
 WHERE a.table_name = 'EXT_SINISTRI_RISCHIO_FRODE'
ORDER BY 4, 5;
```
