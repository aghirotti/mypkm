---
alias: Tutte le info su una tabella
---

```sql
SET ECHO         OFF
SET HEADING      OFF
SET LINE         32767
SET LONG         90000
SET PAGES        0
SET TRIMSPOOL    ON
SET SERVEROUTPUT ON

SPOOL "C:\aubay\tmp\out.sql"

DECLARE
    v_ddl_tab     LONG;
    v_ddl_com     LONG;
    v_ddl_idx     LONG;
    v_ddl_con     LONG;
    v_ddl_rco     LONG;
    v_ddl_tri     LONG;
    v_ddl_gra     LONG;

BEGIN
        -- exec dbms_metadata.set_transform_param (dbms_metadata.session_transform, 'STORAGE',       false);
        -- exec dbms_metadata.set_transform_param (dbms_metadata.session_transform, 'SQLTERMINATOR', true);
        dbms_metadata.set_transform_param (dbms_metadata.session_transform, 'STORAGE',       false);
        dbms_metadata.set_transform_param (dbms_metadata.session_transform, 'SQLTERMINATOR', true);

        dbms_output.put_line ('------------------------------------------------------------');
        dbms_output.put_line ('Tabella: ');
        dbms_output.put_line ('------------------------------------------------------------');
        SELECT dbms_metadata.get_ddl ('TABLE', 'T_SD_PTFDN_FT_DECOMM_CNTR', 'EII_SDW') INTO v_ddl_tab FROM dual;
        dbms_output.put_line (v_ddl_tab);
        dbms_output.put_line ('------------------------------------------------------------');
        ----
        dbms_output.put_line ('commenti');
        dbms_output.put_line ('------------------------------------------------------------');
        BEGIN
            SELECT dbms_metadata.get_dependent_ddl ('COMMENT', table_name) INTO v_ddl_com
              FROM all_tables WHERE owner = 'EII_SDW' AND table_name = 'T_SD_PTFDN_FT_DECOMM_CNTR';

            EXCEPTION
                WHEN OTHERS THEN NULL;
        END;
        dbms_output.put_line (v_ddl_com);
        dbms_output.put_line ('------------------------------------------------------------');
        ----
        dbms_output.put_line ('indici');
        dbms_output.put_line ('------------------------------------------------------------');
        BEGIN
            SELECT dbms_metadata.get_dependent_ddl ('INDEX', 'T_SD_PTFDN_FT_DECOMM_CNTR', 'EII_SDW') INTO v_ddl_idx FROM dual;

            EXCEPTION
                WHEN OTHERS THEN NULL;
        END;
        dbms_output.put_line (v_ddl_idx);
        dbms_output.put_line ('------------------------------------------------------------');
        ----
        dbms_output.put_line ('constraints');
        dbms_output.put_line ('------------------------------------------------------------');
        BEGIN
            SELECT dbms_metadata.get_dependent_ddl ('CONSTRAINT', 'T_SD_PTFDN_FT_DECOMM_CNTR', 'EII_SDW') INTO v_ddl_con FROM dual;

            EXCEPTION
                WHEN OTHERS THEN NULL;
        END;
        dbms_output.put_line (v_ddl_con);
        dbms_output.put_line ('------------------------------------------------------------');
        ----
        dbms_output.put_line ('ref constraints');
        dbms_output.put_line ('------------------------------------------------------------');
        BEGIN
            SELECT dbms_metadata.get_dependent_ddl ('REF_CONSTRAINT', 'T_SD_PTFDN_FT_DECOMM_CNTR', 'EII_SDW') INTO v_ddl_rco FROM dual;

            EXCEPTION
                WHEN OTHERS THEN NULL;
        END;
        dbms_output.put_line (v_ddl_rco);
        dbms_output.put_line ('------------------------------------------------------------');
        ----
        dbms_output.put_line ('triggers');
        dbms_output.put_line ('------------------------------------------------------------');
        BEGIN
            SELECT dbms_metadata.get_dependent_ddl ('TRIGGER', 'T_SD_PTFDN_FT_DECOMM_CNTR', 'EII_SDW') INTO v_ddl_tri FROM dual;

            EXCEPTION
                WHEN OTHERS THEN NULL;
        END;
        dbms_output.put_line (v_ddl_tri);
        dbms_output.put_line ('------------------------------------------------------------');
        ----
        dbms_output.put_line ('grants');
        dbms_output.put_line ('------------------------------------------------------------');
        BEGIN
            SELECT dbms_metadata.get_dependent_ddl ('OBJECT_GRANT', 'T_SD_PTFDN_FT_DECOMM_CNTR', 'EII_SDW') INTO v_ddl_gra FROM dual;

            EXCEPTION
                WHEN OTHERS THEN NULL;
        END;
        dbms_output.put_line (v_ddl_gra);
        dbms_output.put_line ('------------------------------------------------------------');
END;
/

SPOOL OFF
```


