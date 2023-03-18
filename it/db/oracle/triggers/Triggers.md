---
alias: Triggers
---
#oracle_triggers #oracle_sql #oracle 


Tratto da queste [dd queries](https://dataedo.com/kb/query/oracle). Molto interessanti

#### Trigger dell'utente

```sql
SELECT owner             AS trigger_schema_name
     , trigger_name
     , trigger_type
     , triggering_event
     , table_owner       AS schema_name
     , table_name        AS object_name
     , base_object_type  AS object_type
     , status
     , trigger_body      AS script
  FROM sys.all_triggers
       -- excluding some Oracle maintained schemas
 WHERE OWNER NOT IN (
                      'ANONYMOUS'             , 'APEX_040000'
                    , 'APEX_PUBLIC_USER'      , 'CTXSYS'
                    , 'DBSNMP'                , 'DIP'
                    , 'EXFSYS'                , 'FLOWS_30000'
                    , 'FLOWS_FILES'           , 'LBACSYS'
                    , 'MDDATA'                , 'MDSYS'
                    , 'MGMT_VIEW'             , 'OLAPSYS'
                    , 'ORACLE_OCM'            , 'ORDPLUGINS'
                    , 'ORDSYS'                , 'OUTLN'
                    , 'OWBSYS'                , 'PUBLIC'
                    , 'SI_INFORMTN_SCHEMA'    , 'SPATIAL_CSW_ADMIN_USR'
                    , 'SPATIAL_WFS_ADMIN_USR' , 'SYS'
                    , 'SYSMAN'                , 'SYSTEM'
                    , 'TSMSYS'                , 'WKPROXY'
                    , 'WKSYS'                 , 'WK_TEST'
                    , 'WMSYS'                 , 'XDB'
                    , 'XS$NULL'
)
ORDER BY trigger_name
       , table_owner
       , table_name
       , base_object_type;
```
