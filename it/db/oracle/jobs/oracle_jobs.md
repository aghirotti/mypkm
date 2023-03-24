---
alias: Oracle Jobs
tags: oracle_jobs, oracle, v$session, gv$session
---

### Creazione
``` sql
DBMS_SCHEDULER.CREATE_JOB(
	job_name => 'JOB_PKG_ETL_CLMDETS_MAIN',
	job_type => 'STORED_PROCEDURE',
	job_action => 'GW_CLAIM_STG.PKG_ETL_CLMDETS.PRC_MAIN_CLMDETS'
)
```

### Esecuzione
``` sql
BEGIN
    DBMS_SCHEDULER.RUN_JOB(job_name => '"GW_CLAIM_STG"."JOB_PKG_LOAD_PDW_MAIN"', USE_CURRENT_SESSION => FALSE);
END;
```

### Abilitare/disbilitare un job
``` sql
BEGIN
    -- Abilitare
    dbms_scheduler.enable (name=>'"ITSMS"."JOB_FIND_RECLAMI"');
    dbms_scheduler.enable (name=>'"ITSMS"."JOB_GDPR_MASCHERAMENTO_DATI"');
    
    -- Disabilitare
    dbms_scheduler.disable (name=>'"ITSMS"."JOB_FIND_RECLAMI"'             , force => TRUE);
    dbms_scheduler.disable (name=>'"ITSMS"."JOB_GDPR_MASCHERAMENTO_DATI "' , force => TRUE);
END;
```






### Controllo
Se sappiamo il nome del job possiamo eseguire la seguente query, che é la stessa che viene eseguita da SqlDeveloper; questo strumento permette, in più, di sapere quale statement sql tra i tanti il nostro job sta eseguendo; allo scopo basta selezionare la riga ottenuta da questa query per vedere i dettagli nella finestra sottostante.
``` sql
WITH vs AS (
            SELECT rownum AS rnum
                 , inst_id
                 , sid
                 , serial#
                 , status
                 , username
                 , last_call_et
                 , command
                 , machine
                 , osuser
                 , module
                 , action
                 , resource_consumer_group
                 , client_info
                 , client_identifier
                 , type
                 , terminal
                 , sql_id
                 , sql_child_number
              FROM gv$session
           )
SELECT vs.inst_id       AS INST_ID
     , vs.sid           AS SID
     , serial#          AS SERIAL
     , vs.sql_id        AS SQL_ID
     , vs.sql_child_number
     , vs.username      AS USERNAME
     , CASE
           WHEN vs.status = 'ACTIVE' THEN last_call_et 
           ELSE NULL
       END              AS "SECONDS IN WAIT"
     , (SELECT command_name FROM v$sqlcommand WHERE command_type = vs.command) "COMMAND"
     , vs.machine       AS "MACHINE"
     , vs.osuser        AS "OS USER"
     , lower(vs.status) AS "STATUS"
     , vs.module        AS "MODULE"
     , vs.action        AS "ACTION"
     , vs.resource_consumer_group
     , vs.client_info
     , vs.client_identifier
  FROM vs 
 WHERE vs.username IS NOT NULL
   AND nvl(vs.osuser,'x') <> 'SYSTEM'
   AND vs.type            <> 'BACKGROUND'
   AND vs.action           = 'JOB_PKG_LOAD_PDW_MAIN'
ORDER BY 1, 2, 3;
```
