---
alias: Alter Table
tags: oracle_sql, sql, alter_table, oracle
---
# ALTER TABLE

Sul comando vedi anche questo [sito](https://docs.oracle.com/javadb/10.6.2.1/ref/rrefsqlj81859.html)


### Definire una colonna UNUSED

Vedi [[it/db/oracle/tabelle/unused_cols|Colonne non usate in una tabella]]


### Aggiungere un vincolo di tipo pk/fk

``` sql
ALTER TABLE <owner>.<table_name>
      ADD CONSTRAINT <nome_constraint> PRIMARY KEY  (col1, col2, col3.....);

ALTER TABLE <owner>.<table_name>
      ADD CONSTRAINT <nome_constraint> FOREIGN KEY (col1, col2, ...) REFERENCES <owner>.<tabella> (col1, col2, ....) ENABLE;

```

### Rinominare una colonna

``` sql
ALTER TABLE <owner>.<table_name> RENAME COLUMN <name> TO <new name>;
```
   
### Aggiungere una o più colonne

``` sql
ALTER TABLE <owner>.<table_name> ADD <colonna> VARCHAR2 (3 CHAR);

ALTER TABLE <owner>.<table_name> ADD (
     column1 VARCHAR2 (3 CHAR)
    ,column2 VARCHAR2 (3 CHAR)
    ,column3 VARCHAR2 (3 CHAR)
);
```   

### Rinominare una colonna di tabella/vista

``` sql
ALTER TABLE <owner>.<table_name> RENAME COLUMN <column_name> TO <new column_name>;
```

oppure

``` sql
RENAME <table_name> TO <new_table_name>;
```

Se sono nel mio schema e sono il proprietario della tabella le due forme sono indifferenti. Il comando RENAME non funziona se davanti al nome tabella specifico il nome dello schema. Per le viste funziona solo il RENAME.

-

### Modificare una o più colonne:

``` sql
ALTER TABLE <owner>.<table_name> MODIFY (<col1> NULL, <col2> NULL, .....);

ALTER TABLE eii_sdw.t_sd_cli_ft_sint_danni MODIFY (
      flg_ultra               DEFAULT 0
     ,nr_contr_ultra          DEFAULT 0
     ,imp_premi_danni_ultra   DEFAULT 0
     ,flg_ultra_nativo        DEFAULT 0
     ,flg_ultra_decommission  DEFAULT 0
);
```



### Eliminare una colonna:(zs

``` sql
ALTER TABLE <owner>.<table_name> DROP COLUMN <column name>;
```


### Troncare una partizione:

``` sql
ALTER TABLE <owner>.<table_name> TRUNCATE PARTITION <nome partizione>
```

Se la tabella é partizionata (per lista) e ha una PK il comando precedente lascia gli indici in una situazione instabile, per cui bisogna usare

``` sql
ALTER TABLE <owner>.<table_name> TRUNCATE PARTITION <nome partizione> UPDATE INDEXES;
```
