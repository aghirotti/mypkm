---
alias: Obsidian plugins
tags: obsidian, plugins, dataview, templater
---


### Dataview

#### Links
[Un ottimo articolo su dataview](https://denisetodd.medium.com/obsidian-dataview-for-beginners-a-checklist-to-help-fix-your-dataview-queries-11acc57f1e48)
[Video introduttivo su Dataview](https://www.youtube.com/watch?v=8yjNuiSBSAM)
[Dataview documentation](https://blacksmithgu.github.io/obsidian-dataview/queries/structure/)

#### Note
Ci sono tre formati di output: TABLE, LIST e TASK, ovvero il nostro risultato può avere ò'aspetto di una tabella, di una lista o di un task, Se diamo solo il comando LIST avremo una lista di tutte le note presenti nel nostro vault; lo stesso con il comando TABLE, ma la tabella, a differenza della lista, deve avere una testata, sulla quale si possono usare gli alias, esattamente come in SQL.
La query mostra per definizione il nome del file e le altre colonne se le abbiamo definite nei metadati del formato YAML del file; se nei metadato abbiamo definito una riga a nome **notetype** e scriviamo la parola notetype a destra di TABLE la query restituirà i valori corretti dove presenti. NB: é diverso scrivere _notetype_ e _Notetype_, nel secondo caso la query non restituirà nulla.

il FROM individua l'insieme dei dati da cui leggere le informazioni:
- FROM #tag1 AND #tag2 ci dà tutte le note che hanno entrambi i tag
- FROM -tag1 (senza #) ci dà tutte le note che NON contengono tag1
- FROM "<nome cartella>" tutte le note che si trovano in quella cartella
- FROM [[<nome della pagina>]] sono gli incoming link della pagina
- FROM outgoing{[[<nome della pagina>]]} sono gli outgoing link

- WHERE serve per filtrare i dati, ad es. WHERE file.name = "<nome del file>" o != per diverso
- WHERE file.size > 2000 sono tutte le note aventi dimensione maggiore di 2000 bytes
- WHERE contains (author, "<nome autore>")

Il formato generale di una query é il seguente:
![[Schermata 2023-03-05 alle 10.26.16.png]]
#### Fields
A field has two parts: the field-name and the field-value. The format of a field is:  
**field-name:: field-value**

In addition, fields can be defined in the  
1) body of your note — called Inline-fields; or  
2) front matter of your note — called YAML-fields.

Although functionally they are practically the same, they do have slightly different formatting rules that are mentioned throughout this article. Think of a **field-name** like you would column headers in a report.

#### Implicit Fields

Behind the scene, Dataview assigns certain field names and values to each of your notes. You don’t see them, but you can use them. Most are especially helpful when using the WHERE filter (see below).

A complete [list of Implicit fields is here,](https://blacksmithgu.github.io/obsidian-dataview/data-annotation/#implicit-fields_1) but the ones I use most are:

-   file.name = title of your note
-   file.folder = the folder where your note is located
-   file.cdate = the date the file was created
-   file.mdate = the date the file was last modified
Note: you cannot use implicit fields with the FROM filter.

### Templater
[Using the Obsidian Templater Plugin](https://www.youtube.com/watch?v=5j9fAvJCaig)
