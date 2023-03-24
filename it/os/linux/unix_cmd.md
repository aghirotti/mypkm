---
alias: Comandi unix
---
#unix #unic_cmd

### date

#### Es1
```sh
date '+DATE: %m/%d/%y%nTIME:%H:%M:%S'
```
 produce
```sh
DATE: 02/08/23
TIME:14:25:52
```
 
#### Es2
```sh
date '+%Y%m%d:%H%M'
```
 produce
```sh
20230208:1433
```
 


### scp

```
scp -rp oracle@itsmsdbprod:/oradata/itsms/script/* ./
cd DBA/scripts
scp -rp oracle@itsmsdbprod:/home/oracle/DBA/scripts/* ./
```