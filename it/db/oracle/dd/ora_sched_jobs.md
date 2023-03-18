---
alias: Oracle scheduled jobs
tags: oracle_dd, dd, oracle,  oracle_jobs, schedulazione
notetype: sql_code
sqltable: all_scheduler_jobs
---

Tratto da queste [dd queries](https://dataedo.com/kb/query/oracle). Molto interessanti

## Query

```sql
SELECT owner              AS SCHEMA_NAME
     , job_name           AS JOB_NAME
     , job_style          AS JOB_STYLE
     , CASE WHEN job_type IS NULL  
                 THEN 'PROGRAM'
            ELSE job_type
       END                AS JOB_TYPE  
     , CASE WHEN job_type IS NULL 
                 THEN program_name
            ELSE job_action
       END                AS JOB_ACTION
     , start_date         AS START_DATE
     , CASE WHEN repeat_interval IS NULL
                 THEN schedule_name
            ELSE repeat_interval
       END                AS schedule
     , last_start_date    AS LASS_START_DATE
     , next_run_date      AS NEXT_RUN_DATE
     , state              AS STATE
  FROM sys.all_scheduler_jobs
ORDER BY owner, job_name
```