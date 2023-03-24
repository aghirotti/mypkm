---
alias: Usare IPhone come webcam
tags: apple, iphone, webcam
type: telefonia
---

Tratto dal sito [https://www.youtube.com/watch?v=Epfa9WfCC58](https://www.youtube.com/watch?v=Epfa9WfCC58). Configurato e testato sul mio MacPro.
Senza aspettare Ventura è possibile utilizzare il proprio smartphone come webcam in servizi di teleconferenza come Teams o Zoom. Il funzionamento necessita di un sito ([https://vdo.ninja](https://vdo.ninja/)) che permette la condivisione del flusso video di Iphone e di un sw di registrazione video a nome OBS Studio ([https://obsproject.com/](https://obsproject.com/)).
Colleghiamoci al sito [sito](https://vdo.ninja/) verrà generato un QR Code come in figura, insieme ad un URL che utilizzeremo poi nel browser
Da IPhone inquadriamo il QR code e apriamo il code con Safari o Chrome
Scarichiamo OBS Studio dal [sito](https://obsproject.com/), individuiamo la sezione Fonti e click sul + per scegliere Browser
Diamo un nome alla nuova fonte, poi apriamo le Proprietà e, nella riga URL, inseriamo quanto compare in OBS Browser Source Link.
Regoliamo altezza e larghezza dello schermo ai valori opportuni
Apriamo Teams e ci colleghiamo alla riunione, apriamo le Preferenze e poi andiamo su Devices, scroll fino a trovare la voce Camera e scegliamo OBS Virtual Camera