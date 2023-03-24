---
alias: Informazioni sul db
---
#oracle #oracle_howto  #oracle_info_db #unpivot

# Informazioni sul db
```sql
COL NAME FORMAT A30
COL VAL  FORMAT A30

SELECT a.*
  FROM (
        SELECT *
          FROM (
                SELECT
                       sys_context ('USERENV', 'CURRENT_SCHEMA'  ) AS CURRENT_SCHEMA
                     , sys_context ('USERENV', 'CURRENT_SCHEMAID') AS CURRENT_SCHEMA_ID
                     , sys_context ('USERENV', 'CLIENT_INFO'     ) AS CLIENT_INFO
                     , sys_context ('USERENV', 'DB_NAME'         ) AS DB_NAME
                     , sys_context ('USERENV', 'DB_UNIQUE_NAME'  ) AS DB_UNIQUE_NAME
                     , sys_context ('USERENV', 'SESSION_USER'    ) AS SESSION_USER
                     , sys_context ('USERENV', 'SESSION_USERID'  ) AS SESSION_USERID
                     , sys_context ('USERENV', 'NLS_DATE_FORMAT' ) AS NLS_DATE_FORMAT
                  FROM dual
                 WHERE sys_context ('USERENV', 'SESSIONID') NOT IN ('SYS', 'XDB')
               )
        UNPIVOT INCLUDE NULLS (
                               val FOR NAME IN (
                                                 current_schema
                                               , current_schema_id
                                               , client_info
                                               , db_name
                                               , db_unique_name
                                               , SESSION_USER
                                               , session_userid
                                               , nls_date_format
                                               )
                              )
       ) a
 --WHERE val IS NOT NULL
ORDER BY NAME;
```

