---
alias: Statistiche su una tabella
---
#dbms_stats #ora_statistiche #analyze_table #oracle #oracle_howto 


``` sql
BEGIN
    dbms_stats.gather_table_stats(
        ownname          => 'DMTADMINDEV'
       ,tabname          => 'FCTTBLCSTR02_CON_IT_YY'
       ,estimate_percent => dbms_stats.auto_sample_size
    );
END;
```