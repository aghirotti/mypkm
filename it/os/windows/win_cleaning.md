---
alias: Pulizia del sistema
---


## Debloating
Questo termine significa togliere dalla nostra intallazione Win10 o win11 tutto il cosidetto bloat, ovvero il rigonfiamento, cioè tutti quei sw che Microsoft installa per i propri scopi, come la telemetria, oppure parti di sw che o noi non servono, come OneNote. Queste note si basano su questo filmato, [Potenziare e pulire Windows in un minuto](https://www.youtube.com/watch?v=HRh_MgoApNY). Il sito in inglese é [questo](https://christitus.com/one-tool-for-everything/), mentre [questa](https://www.youtube.com/watch?v=vXyMScSbhk4) é la presentazione dell'autore, Chris Titus.

Per prima cosa vanno tenuti presenti questi tre concetti:
a) tutto questo va fatto su una macchina nuova, su cui Windows é appena stato installato
b) non tutti gli strumenti che vedremo sono necessari, esiste un percorso guidato altamente consigliabile
c) per usare questo tool occorre passare da PowerShell, ovviamente eseguito come amministratore.

## Lo strumento
Lo script che useremo è sviluppato da Chris Titus, un creator americano con oltre 20 anni di esperienza in ambito IT. Il suo progetto è totalmente open-source, costantemente aggiornato e non ci chiede di eseguire nessun file .exe. Questo é il suo [repository su GitHub.](https://github.com/ChrisTitusTech/winutil)
- Aprire PowerShell come admin e dare questo comando irm christitus.com/win \| iex
