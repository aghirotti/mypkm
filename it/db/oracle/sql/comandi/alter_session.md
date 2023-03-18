---
alias: Alter session
tags: sql, oracle_sql, alter_session, oracle, ddl
---

Il comando ALTER SESSION é considerato un comando DDL.

```sql
SELECT substr (value, 1, 1)  AS SEPARATOR
     , 'using NLS-PARAMETER' AS EXPLANATION
  FROM nls_session_parameters  
 WHERE parameter = 'NLS_NUMERIC_CHARACTERS'  
UNION ALL  
SELECT substr (0.5, 1, 1) AS SEPARATOR  
     , 'using NUMBER IMPLICIT CASTING' AS Explanation  
  FROM DUAL;
```


```sql
ALTER SESSION SET nls_date_format='DD/MM/YYYY HH24:MI:SS';
ALTER SESSION SET nls_numeric_characters = ',.';
ALTER SESSION SET nls_territory='Italy';
ALTER SESSION SET current_schema=......;
```

