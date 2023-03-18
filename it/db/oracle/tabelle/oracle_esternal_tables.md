---
alias: Oracle external tables
---
#oracle #oracle_external_tables

### File in input
```sql
ESERCIZIO;MESE;PREMI 4R ;PREMI 2R
2022;1;10,30;5,65
2022;2;20,89;12,70
2022;3;30,55;24,00
2022;4;40,82;22,35
2022;5;50,73;28,12
2022;6;60,00;30,23
2022;7;70,55;37,06
2022;8;80,21;33,00
2022;9;90,74;54,87
2022;10;100,99;88,66
2022;11;110,66;55,88
2022;12;120,31;119,00
```

### Tabella esterna
```sql
CREATE TABLE dwh_finance.ext_premi_contab (
    esercizio        NUMBER (4)
   ,mese             NUMBER (2)
   ,premi_4r         VARCHAR2 (16)
   ,premi_2r         VARCHAR2 (16)
) 
ORGANIZATION EXTERNAL (
    TYPE ORACLE_LOADER
    DEFAULT DIRECTORY "BOLLATI_FINANCE_DIR"
    ACCESS PARAMETERS (
                       RECORDS DELIMITED BY '\r\n'
                       BADFILE BOLLATI_FINANCE_DIR:'reg79_input_premi_2022.bad'
                       LOGFILE BOLLATI_FINANCE_DIR:'reg79_input_premi_2022.log'
                       DISCARDFILE BOLLATI_FINANCE_DIR:'reg79_input_premi_2022.dsc'
                       SKIP 1
                       FIELDS TERMINATED BY ';'
                      )
    LOCATION (BOLLATI_FINANCE_DIR:'reg79_input_premi_2022.csv')
)
REJECT LIMIT UNLIMITED;
```

#### GRANTS
ATTENZIONE: NON é possibile assegnare grant di  ins / upd / delete su una tabella esterna ad un altro utente. Nel caso della tabella usata come esempio qui sopra possiamo eseguire
```sql
GRANT SELECT ON ext_sinistri_rischio_frode TO DWH_CLAIM_CARD_STG;
```
ma non possiamo fare questo
```sql
GRANT INSERT, UPDATE; DELETE ON ext_sinistri_rischio_frode TO DWH_CLAIM_CARD_STG;
```
