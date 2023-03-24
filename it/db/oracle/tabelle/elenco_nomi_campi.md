---
alias: Elenco nomi campi della tabella separato da virgola
---
#oracle_sql #oracle #oracle_tables #oracle_howto

```sql
SELECT listagg (col, ', ') WITHIN GROUP (ORDER BY col_id) AS LISTA_COLONNE
  FROM (
        SELECT lower (column_name) AS COL
             , column_id           AS COL_ID
          FROM all_tab_columns
         WHERE table_name = 'ANIA_INFORTUNI'
        ORDER BY column_id
       );
```
