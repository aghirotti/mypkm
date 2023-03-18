---
alias: Sincronizzare un repository git 
---
Seguire i seguenti passi se si vuole lavorare con LogSeq su due o più dispositivi, ad es su Mac e Win, dove Win é la macchina aziendale e Mac é il mio pc personale
-   Creare un account su [GitHub](https://github.com/)
    -   Il mio account ha come username/pwd i valori `aghirotti/albicocca2015`
- Installare su ogni macchina il sw [Git Credential Manager](https://github.com/GitCredentialManager/git-credential-manager/blob/release/docs/install.md)
- Installare su entrambe le macchine il sw git, in modo da poter disporre del comando `git` dalla CLI. In particolare in Windows ciò avviene installando la [git shell for windows](https://gitforwindows.org/) che fornisce un completo ambiente `bash`
- Collegarsi al proprio account git e creare un nuovo repository a nome `z_ls`, pubblico o privato non ha importanza, e non aggiungere altro
- Sul Mac aprire il terminale e posizionarsi nella dir dove risiede il grafo di LogSeq `cd /Users/alberto/Library/CloudStorage/Dropbox/z_ls`
- Eseguire le seguenti istruzioni

echo "Sono un repository" >> README.md

```
git init  
git add README.md  
git commit -m "first commit"  
git branch -M main  
git remote add origin [https://github.com/aghirotti/z_ls.git](https://github.com/aghirotti/z_ls.git)  
git push -u origin main  
```
  
Spostarsi sulla macchina Windows in `/c/Users/aghirot/Documents/`
Eseguire il comando `git clone https://github.com/aghirotti/z_ls.git` per scaricare tutto il repository in locale
Aprire LogSeq e aprire il grafo presente nella cartella `z_ls` appena scaricata
Lavorare sulla macchina Windows
Per sincronizzare dalla bash usare il comando `git push`
Spostarsi sul Mac e da terminale dare il comando `git pull`