---
alias: Mac comandi da terminale
---
[50 macOS Tips and Tricks Using Terminal](https://www.youtube.com/watch?v=qOrlYzqXPa8/)

# caffeinate
Pausa caffè del Mac, il terminale si ferma e non fa più nulla, si interrompe con `CTRL - C`

# defaults
Serve in varie occasioni, ad es.
- per cambiare il nome di default con cui il Mac salva lo screenshot
        `defaults write com.apple.screencapture name "<nuovo nome"`
- per cambiare il tipo di immagine dello screenshot
        `defaults write com.apple.screencapture type jpg`
- per cambiare ls posizione dove salva il file
        `defaults write com.apple.screencapture location "<nuova posizione>"`

# pbcopy
Questo comando va usato in pipe con altri e permette di copiare negli appunti il risultato del comando precedente; ad es. `ls -la | pbcopy` poi posso fare il paste in una mail o in altre applicazioni.