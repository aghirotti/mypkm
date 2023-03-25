---
alias: Vim Howto
tags: sw, vim, vim_howto, #vimsession
---
## Gestione degli spazi

##### Sostituire uno o più spazi con niente
``` sql
:%s/\s\s+//g
```
##### Eliminare gli spazi a fine riga
``` sql
:%s/\s\+$//
```
| Cmd    | Spiegazione                                                                               | 
| ------ | ----------------------------------------------------------------------------------------- |
| **:**  | serve per entrare in modalità comando ed                                                  |
| **%**  | indica di agire sulle righe dell'intero file                                              |
| **/**  | delimita l'inizio del testo da cercare                                                    |
| **\s** | indica gli spazi o i caratteri di tabulazione                                             |
| **\+** | definisce la quantità di caratteri definito da **\s** ovvero 1 o più                      |
| $      | indica che il testo cercato deve trovarsi a fine riga                                     |
| **/**  | delimita la fine del testo da cercare e l'inizio del testo da sostituire a quello cercato |
| **/**  | delimita la fine del testo da sostituire a quello cercato                                 |

## Sessioni
##### Crea un file sessione
``` sh
:mks <path>/mia_sessione.vim
```
##### Carica una sessione
``` sh
:source <path>/mia_sessione.vim
```