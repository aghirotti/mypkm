---
alias: Oggetti che usano uno specifico oggetto
tags: oracle, oracle_dd, all_dependecies
notetype: sql_code
sqltable: all_dependencies
---

Tratto da queste [dd queries](https://dataedo.com/kb/query/oracle). Molto interessanti

## Query

```sql
  SELECT owner || '.' || name                     AS referencing_object
     , type                                       AS referencing_type
     , referenced_owner || '.' || referenced_name AS referenced_object
     , referenced_type
  FROM sys.all_dependencies
 WHERE referenced_name  = 'AGGR_SIN_GEST_TBL'
   --AND referenced_owner = ''
ORDER BY referencing_object;
```


| Colonna | Significato |
|:--- |:--- |
| referencing_object | provided object name with schema name |
| referencing_type | type of provided object |
| referenced_object | name and schema of the referenced object |
| referenced_type | type of referenced object |

One row represents one depending object
Scope of rows: all objects that are depending on specified object ordered by referencing object schema name and name
