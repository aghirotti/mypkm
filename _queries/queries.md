---
alias: Queries
---




### q1

```dataview
TABLE without ID file.link AS NOME, alias AS ALIAS, notetype AS TIPO_NOTA
 FROM #oracle 
WHERE sqltable="all_dependencies" OR notetype="sql_code"
 SORT nome ASC
```


### q2


```dataview
LIST
FROM "hints"
```

##3 q2

```dataview
LIST FROM #oracle 
```