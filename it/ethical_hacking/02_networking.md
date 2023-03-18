---
alias: Ethical Hacking - Networking
---
# IP Address

Il comando `ipconfig`(Windows) o `ifconfig` (mac e linux) permette di vedere qual'è in nostro ind. IP su quella interfaccia, sia per la versione IPv4 (riga inet nella fig. sotto) che per la IPv6 (riga inet6).

![](app://local/Users/alberto/Library/CloudStorage/Dropbox/bd_tech_notes/files/immagini/if_config.png?1670509234119)

Come si vede l'ind. IP in v. 4 é espresso in notazione decimale, mentre quello in v. 6 é espresso in notazione esadecimale. Un ind. IP rappresenta il modo in cui comunichiamo, e si pone, perciò. al liv, 3 del modello OSI
Ogni gruppo di cifre nella notazione decimale dell'ind. IP rappresenta un gruppo di 8 bit, che valgono 0/1, quindi abbiamo 32 bit, o 4 bytes, con questo metodo possiamo avere al massimo 2^32 = 4.294.967.296 ind. IP distinti, che, oggi, non sono sufficienti. Per questo motivo é stato inventato il sistema IPv6, basato su 128 bit, per cui in questo modo avremo 2^128 = 2.4 10E38, cioé un numero enormemente maggiore.
Tuttavia tutti continuano ad usare il sistema IPv4 anche se gli indirizzi sono esauriti. Questo é possibile grazie al NAT (Network Address Translation). Difatti tutti gli ind. IP che iniziano per 192.168 sono fittizi, ovvero non sono uno del circa 4 m.di di ind. IP disponibili, bensì passano attraverso un ind. IP pubblico.
Dalla tabella seguente vediamo che gli ind. IP di tipo 192.168 sono di classe C e tutti i dispositivi della nostra rete locale comunicano con l0esterno tramite un solo ind. IP, quello del nostro fornitore internet, Telecom o Vodafone che sia.

![[Schermata 2023-03-12 alle 09.06.09.png]]
    
Questa tecnica permette di utilizzare gli ind. IP v4 per la stragrande maggioranza degli usi senza necessità di usare gli IP v.6. Poiché tutto questo appartiene al livello 3 OSI, che si occupa degli indirizzamenti (router), possiamo dire che noi indirizziamo il traffico di rete (we route, in inglese) tramite gli indirizzi IP.
Un ottimo [articolo](https://www.freecodecamp.org/italian/news/maschere-di-sottorete-24-30-26-27-29-e-altri-riferimenti-per-indirizzi-ip-e-cidr/) sulle maschere di sottorete.
