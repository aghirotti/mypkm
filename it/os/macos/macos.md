---
alias: MacOs come si comporta
---

### Cosa abbiamo scaricato

Lo sapevate che il Mac tiene traccia di tutto ciò che abbiamo scaricato da Internet, anche se abbiamo pulito la cronologia del browser? Queste informazioni sono memorizzate in un db sqlite3 che si può interrogare con questo comando

`sqlite3 /Users/alberto/Library/Preferences/com.apple.LaunchServices.QuarantineEventsV2 'SELECT LSQuarantineDataURLString FROM LSQuarantineEvent'`

Per cancellare questi dati

`sqlite3 /Users/alberto/Library/Preferences/com.apple.LaunchServices.QuarantineEventsV2 'DELETE FROM LSQuarantineEvent'`
