---
alias: PSQL
---
#postgres #psql

Il comando `psql` è il client da terminale che dà accesso ad una **console testuale di PostgreSQL** in cui si possono usare liberamente direttive SQL o alcuni comandi. I seguenti saranno particolarmente utili:

`psql -d <nome del db>` apre `psql` e usa il database specificato

| Comando | Descrizione |
| --- | --- | 
| `list` | elenca i database disponibili per il profilo utente |
| `dt`| elenca tabelle all'interno del singolo database|
|`z`| elenca tutti gli elementi interni al database, tra cui tabelle e viste|
|`h`| mostra l'aiuto in linea|
|`conninfo`| fornisce informazioni sulla connessione in corso al database|
|`q`| chiude _psql_|
