---
alias: Calcolo spazio occupato da una tabella
tags: #oracle #tabella #spazio_occupato #oracle_sql 
---

```sql
SELECT s.segment_name
     , sum (bytes) / (1024 * 1024) AS table_size_meg
  FROM user_extents s
 WHERE s.segment_type = 'TABLE'
   AND s.segment_name = 'DWT_FT_CLMDETS'
GROUP BY s.segment_name;
```

Questa query funziona solo se la tabella é entrata negli user_extents