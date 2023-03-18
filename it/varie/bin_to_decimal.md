---
alias: Conversione decimale binario
---
#sist_binario #conversioni

## Da decimale a binario

Dividere il numero per 2 e considerare il resto della divisione, ripetendo N volte finché non si arriva a 0. Scrivere i resti da destra verso sinistra usando 8 posizioni.

#### Esempio 1: 65 in binario
```sql
65/2 = 32 con resto 1, 32 / 2 ha resto 0, 16 / 2 ha resto 0, 8 / 2 ha resto 0, 4 / 2 ha resto 0, 2 / 2 ha resto 0, 1 / 2 ha resto 1`
```
Quindi avremo `1000001`

#### Esempio 2: 77 in binario
```sql
77/2 = 38 con resto 1, 38 / 2 ha resto 0, 19 / 2 ha resto 1, 9 / 2 ha resto 1, 4 / 2 ha resto 0, 2 / 2 ha resto 0, 1 / 2 ha resto 1`
```
Quindi avremo `1001101`

## Da binario a decimale

Si moltiplica il valore 1 o 0 per la potenza di 2 espressa dalla posizione della cifra, dove il primo carattere del numero binario ha potenza 7 e l'ultimo a destra ha potenza 0

#### Esempio
Il primo 1 da sinistra è la potenza settima, l'ultimo a dx è la potenza 0

```sql
11010111 = 1*2^7+1*2^6+0*2^5+1*2^4+0*2^3+1*2^2+1*2^1+1*2^0 = 128+64+0+16+0+4+2+1 = 215

01100100 = 0+1*2^6+1*2^5+0+0+1*2^2+0+0 = 100
```
