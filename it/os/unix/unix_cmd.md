---
alias: Comandi unix
tags: unix, unix_cmd, find
---
# date
```sh
date '+DATE: %m/%d/%y%nTIME:%H:%M:%S'
DATE: 02/08/23
TIME:14:25:52

date '+%Y%m%d:%H%M'
20230208:1433
```
 
# find
E 'una funzione ricorsiva che si usa in questo modo'
```sh
# Trova tytti i file aventi estensione .php; la i di iname significa ignorecase
find -type f -iname "*.php"
```


```sh
```


# scp
```sh
scp -rp oracle@itsmsdbprod:/oradata/itsms/script/* ./
cd DBA/scripts
scp -rp oracle@itsmsdbprod:/home/oracle/DBA/scripts/* ./
