---
alias: il comando case
---
#plsql #oracle


Quando in Oracle si  usa uno statement CASE si deve SEMPRE  mettere il ramo ELSE in  modo  da  coprire  tutti  i  casi;  senza  di  esso  il  package  si compila correttamente ma  se,  durante l'esecuzione,  si verifica  un caso  non previsto Oracle  genera  un errore  ORA-06592:  CASE  non  rilevato  durante l'esecuzione dell'istruzione CASE


```sql
CASE
  WHEN (   P_TIPO_OGGETTO = 'C'
        OR P_TIPO_OGGETTO = 'D'
        OR P_TIPO_OGGETTO = 'P') THEN NULL;
  WHEN P_TIPO_OGGETTO = 'Q' THEN NULL;
  WHEN P_TIPO_OGGETTO = 'U' THEN NULL;
  ELSE
    dbms_output.put_line ('CASE - RAMO ELSE - P_TIPO_OGGETTO: ' ||- P_TIPO_OGGETTO);
END CASE;
```


