---
alias: Viste di sistema Oracle
tags: oracle, v$
---

### v$nls_parameters

```sql
COLUMN NAME     FORMAT A20
COLUMN VALUE    FORMAT A28

SELECT DECODE (parameter
              , 'NLS_CHARACTERSET',  'CHARACTER SET'
              , 'NLS_LANGUAGE',      'LANGUAGE'
              , 'NLS_TERRITORY',     'TERRITORY'
              , 'NLS_DATE_FORMAT',   'DATE_FORMAT'
              , 'NLS_DATE_LANGUAGE', 'DATE_LANGUAGE'
              , 'NLS_TIME_FORMAT',   'TIME_FORMAT'
              )      AS NAME
     , value         AS VALUE
  FROM v$nls_parameters
 WHERE parameter IN ('NLS_CHARACTERSET', 'NLS_LANGUAGE', 'NLS_TERRITORY', 'NLS_DATE_FORMAT', 'NLS_DATE_LANGUAGE', 'NLS_TIME_FORMAT')
ORDER BY 1
;

-- In alternativa
SELECT * FROM v$nls_parameters;
```
