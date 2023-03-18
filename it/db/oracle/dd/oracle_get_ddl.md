---
alias: Oracle get_ddl
tags: oracle, oracle_dbms_metadata, oracle_get_ddl
notetype: sql_code
sqltable: get_ddl
---
## La funzione get_ddl

#### Tabelle
``` sql
SET HEADING OFF;
SET ECHO    OFF;
SET PAGES   999;
SET LONG    90000;

SELECT dbms_metadata.get_ddl ('TABLE', '&TABLE_NAME', '&OWNER') FROM dual;
```

#### Indici
``` sql
SET HEADING OFF;
SET ECHO    OFF;
SET PAGES   999;
SET LONG    90000;

SELECT dbms_metadata.get_ddl ('INDEX', '&INDEX_NAME', '&OWNER') FROM dual;
```

#### Viste
``` sql
SET HEADING OFF;
SET ECHO    OFF;
SET PAGES   999;
SET LONG    90000;

SELECT dbms_metadata.get_ddl ('VIEW', '&VIEW_NAME', '&OWNER') FROM dual;
```

#### Packages
``` sql
SET HEADING OFF;
SET ECHO    OFF;
SET PAGES   999;
SET LONG    90000;

SELECT dbms_metadata.get_ddl ('PACKAGE', '&PACKAGE_NAME', '&OWNER') FROM dual;
```

#### Procedures
``` sql
SET HEADING OFF;
SET ECHO    OFF;
SET PAGES   999;
SET LONG    90000;

SELECT dbms_metadata.get_ddl ('PROCEDURE', '&PROCEDURE_NAME', '&OWNER') FROM dual;
```

#### Triggers
``` sql
SET HEADING OFF;
SET ECHO    OFF;
SET PAGES   999;
SET LONG    90000;

SELECT dbms_metadata.get_ddl ('TRIGGER', '&TRIGGER_NAME', '&OWNER') FROM dual;
```

#### Function
``` sql
SET HEADING OFF;
SET ECHO    OFF;
SET PAGES   999;
SET LONG    90000;

SELECT dbms_metadata.get_ddl ('FUNCTION', '&FUNCTION_NAME', '&OWNER') FROM dual;
```

