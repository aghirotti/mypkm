---
alias: Gestire dati nosql con Postgres
---

### Introduzione

Il movimento **NoSQL** prende piede nel 2009 per proporre alternative in grado di superare i limiti dei DBMS, relazionali proponendo forme di archiviazione più flessibili e scalabili.

Il mondo del data storage appare da allora diviso in due grandi emisferi: da un lato l'archiviazione **relazionale** con prodotti open source e proprietari (_MySQL_, _Oracle_, _SQL Server_, eccetera…), dall'altro quello NoSQL con basi di dati non strutturate e totalmente rivolte ai contenuti (_MongoDB_, _OrientDB_, eccetera).

Nonostante ciò, esistono situazioni in cui entrambi gli approcci possono confluire ed integrarsi, come le soluzioni offerte da **PostgreSQL**, un gestore di database molto interessante.

### Il formato JSON in PostgreSQL

Come già accennato, un primo tipo di dati NoSQL viene definito in PostgreSQL mediante **JSON**. Per chi non lo conoscesse, si tratta di un  formato testuale derivato dal linguaggio JavaScript, largamente utilizzato al giorno d'oggi soprattutto nell'interazione tra applicazioni attraverso la rete. Ne fanno uso anche i database NoSQL a documenti, come MongoDB, per la descrizione dei dati.

Riassumendone le caratteristiche, un oggetto JSON è composto da un elenco di proprietà, ognuna specificata da un nome e dal valore assegnatole. Tali   proprietà sono separate da virgole e l'elenco nel suo complesso è racchiuso tra parentesi graffe.
Ad esempio, un oggetto caratterizzato dalle proprietà _nome_, _cognome_, _eta_, rispettivamente valorizzate dai dati “Carlo”, “Rossi” e ”25”, potrebbe essere espresso in JSON così:

```javascript
{ "nome": "Carlo", "cognome": "Rossi", "eta": "25" }
```

All'interno del database _example_, creiamo una tabella di nome _multimedia_ destinata a contenere informazioni su documenti di vario genere (cd musicali, ebook, immagini, eccetera...). Dato che ogni tipo di documento ha le sue peculiarità, la definizione di una struttura rigida, basata sul modello relazionale, potrebbe rivelarsi poco adatta. Utilizziamo pertanto il formato JSON che, per ogni documento, permetterà di utilizzare una stuttura specifica dei dati. Ogni documento sarà descritto da un oggetto JSON.

Una volta fatto accesso al database, creiamo la tabella _multimedia_ con un unico campo denominato _data_ e tipizzato come _JSON_:

```sql
CREATE TABLE multimedia (data JSON);
```

A questo punto inseriamo tre righe, corrispondenti a tre documenti di tipologia diversa:

```sql
INSERT INTO multimedia (data) VALUES ('{"id":"1", "title":"Promessi sposi", "type":"ebook", "pages":"400"}');
INSERT INTO multimedia (data) VALUES ('{"id":"2", "title":"Canzoni di Natale", "type":"CD", "tracks":"12"}');
INSERT INTO multimedia (data) VALUES ('{"id":"3", "title":"panorama.jpg", "type":"photo", "pixels":"1665x894"}');
```

Gli oggetti _JSON_ appena definiti hanno in comune tre proprietà – `id`, `title` e `type` - ma le altre sono specifiche del tipo di documento archiviato.
Sin qui, non sembra niente di eccessivamente innovativo. In fin dei conti, il campo JSON è stato utilizzato in maniera simile ad una stringa. Il vero vantaggio consiste nella possibilità che offre PostgreSQL di **analizzare i dati all'interno del JSON mediante una normale query**.  
Consideriamo, per esempio, la seguente interrogazione:

```sql
SELECT data->>'title' FROM multimedia;
```

Il risultato che produrrà sarà il seguente:

```
Promessi sposi  
Canzoni di Natale  
panorama.jpg  
```

L'operatore `->>` è servito per richiedere a PostgreSQL di analizzare il formato JSON, ed estrapolare i dati del campo _title_. È un po' come se la vera  
tabella fosse ora contenuta nei dati NoSQL, ma rimanesse analizzabile tramite normali dichiarazioni SQL.

### HSTORE, il formato chiave-valore  

Il formato **HSTORE** ricorda una tipologia di dato comunemente nota in informatica come **dizionario**. Ogni informazione viene indicata come una coppia  chiave-valore, ove la chiave è univoca e serve ad indicare il valore corrispondente.
Per usare _HSTORE_ in PostgreSQL, dovremo prima abilitare l'opportuna estensione con la seguente query:
```sql
CREATE EXTENSION hstore;
```

A questo punto, proseguendo l'esempio del paragrafo precedente, creiamo un'ulteriore tabella, che servirà ad abbinare una descrizione ad ogni tipo di dato usato nell'esempio precedente:
```sql
CREATE TABLE data_type (type HSTORE);
```

Inseriamo al suo interno alcune coppie chiave/valore, come mostrato di seguito:
```sql
INSERT INTO data_type VALUES ('"ebook"=>"libro elettronico", "Photo"=>"Immagini in formato digitale", "CD"=>"Compact Disc musicale"');
```

Anche in questo caso, PostgreSQL permette di interrogare i dati all'interno del tipo NoSQL. Si consideri la query seguente:
```sql
SELECT type->'ebook' FROM data_type;
```

Il valore di output che sarà restituito è:
```
libro elettronico
```

### Integrazione tra dati NoSQL ed ANSI SQL  

I tipi _JSON_ e _HSTORE_ mostrano aspetti interessanti almeno per il fatto di poter essere espressi con strutture meno rigide, ed interrogati con le classiche  query SQL. Un aspetto molto interessante è quello di poter utilizzare, in aggiunta a dati tipicamente NoSQL, le più comuni tabelle relazionali, e poter eseguire query "promiscue" all'interno del database.
Dal momento che la tabella _multimedia_, popolata con dati JSON, contiene riferimenti a risorse multimediali molto varie, immaginiamo che un'altra tabella  
custodisca un'infomazione temporale (_timestamp_), che descrive l'ultimo accesso ad una risorsa.

Questa tabella necessita di due campi, ovvero l'id della risorsa in formato testuale, ed il timestamp vero e proprio. In questo caso, possiamo fare a meno della flessibilità del NoSQL; pertanto la creiamo secondo i normali standard di SQL:
```sql
CREATE TABLE log (id TEXT, logtime TIMESTAMP DEFAULT CURRENT_TIMESTAMP);
```

Per default, il timestamp verrà impostato all'ora attuale. Il seguente comando inserirà una riga riferita alla risorsa con _id_ pari a 1:
```sql
INSERT INTO log (id) VALUES ('1');
```

L'id definito coincide con quello riportato nella tabella _multimedia_, quindi possiamo incrociare i dati con un normale join SQL:
```sql
SELECT multimedia.data->>'title' AS title, logtime
FROM multimedia, log
WHERE multimedia.data->>'id'=log.id;
```

L'output prodotto mostrerà due campi, il nome della risorsa (presente nei dati NoSQL della tabella _multimedia_) e il timestamp (presente nella tabella _log_):
```
title | logtime
------------------------------------------------
Promessi sposi | 2014-11-25 17:48:18.535045  
```

Altre tipologie di integrazioni interessanti, questa volta tra dati NoSQL, sono offerte da funzioni già incluse in PostgreSQL che permettono **conversioni e  
trasformazioni di dati JSON e HSTORE**. Un elenco completo con relativi esempi si può reperire facendo riferimento alla [documentazione ufficiale](http://www.postgresql.org/docs/).

### Le prestazioni  

Le capacità NoSQL viste sinora dischiudono prospettive nuove ed interessanti. Il dubbio che può legittimamente sorgere a questo punto riguarda le   prestazioni. Un [recente esperimento svolto da EnterpriseDB Corporation](http://blogs.enterprisedb.com/2014/09/24/postgres-outperforms-mongodb-and-ushers-in-new-developer-reality/) ha confrontato prestazioni e consumo di spazio tra PostgreSQL 9.4 e MongoDB 2.6 nell'immagazzinamento di grandi moli di dati di tipo NoSQL.

Il risultato, sorprendente, è stato nettamente a favore di PostgreSQL. Questo DBMS ha dimostrato infatti una netta superiorità rispetto a MongoDB: 2,1   volte più veloce nell'inserimento di grandi moli di dati, oltre che 2,5 volte più performante nelle operazioni di selezione; il tutto risparmiando il 33% di   spazio.

La tabella seguente mette a confronto i numeri dell'esperimento:
[  
![](https://static.html.it/app/uploads/2014/11/postgres_img01-600x191.png)](https://static.html.it/app/uploads/2014/11/postgres_img01.png)