---
alias: Oracle hints
tags: hints, oracle_hints
---

[Concetti introduttivi](https://renenyffenegger.ch/notes/development/databases/Oracle/SQL/hints/index)

# Oracle SQL Hints

## Introduzione
Most hints are used to influence the [optimizer](https://renenyffenegger.ch/notes/development/databases/Oracle/optimizer/index) and have no effect on the result of an SQL statement exuction. There are three execptions, however, which _do_ have an effect on the result of an SQL statement (but should not `fresh_mv` not also be counted among them?):

-   change_dupkey_error_index
-   ignore_row_on_dupkey_index
-   retry_on_row_change

The hints are formulated within [comments](https://renenyffenegger.ch/notes/development/databases/SQL/statement/comment/index) whose _first character_ is a plus sign (`+`). The comment must be inserted in an [SQL statement](https://renenyffenegger.ch/notes/development/databases/Oracle/SQL/statement/index) directly after the one of the keywords `select`, `update`, `insert`, `delete` or `merge`. In all other places, a comment cannot be be recognized as a hint.

Multiple hints are separated by white space.

```sql
select /*+ hint-1 hint-2 … */
  …
from
  …;
```
A hint can have arguments:
```sql
select /*+ hint(argument)                 */  …
select /*+ hint(argument-1 argument_2 … ) */  …
```
When using _component queries_ (for example when combined with `union`), both queries can have their own hint:
```sql
select /*+ hint-1 */ …
  union
select /*+ hint-2 */ …
```
All hints except `/*+ rule */` cause the [(cost based) optimizer](https://renenyffenegger.ch/notes/development/databases/Oracle/optimizer/index) to be used.

If mutliple hints are specified and a hint is not understood by Oracle (for example because of a typo), then Oracle will honor the hints on the left side of that hint and disregard the rest.

## Four types of hints

|              | **Operates on**                                                                                                      | **Examples**                                                                                                   | **Comment**                                                                                                                                                                                                                                                                                         |
| ------------ | -------------------------------------------------------------------------------------------------------------------- | -------------------------------------------------------------------------------------------------------------- | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Single table | _one_ table or view                                                                                                  | `index(tab ix)` , `use_nl(…)`                                                                                  |                                                                                                                                                                                                                                                                                                     |
| Multi-table  | multiple table                                                                                                       | `[leading](https://renenyffenegger.ch/notes/development/databases/Oracle/SQL/hints/list/leading)(tab_a tab_b)` |                                                                                                                                                                                                                                                                                                     |
| Query-block  | single [query blocks](https://renenyffenegger.ch/notes/development/databases/Oracle/SQL/statement/query-block/index) | `star_transformation(@sel$2)` , `unnest(@sel$2)` , `full(@sel$2 t1)`                                           | Compare with the column [`qblock_name`](https://renenyffenegger.ch/notes/development/databases/Oracle/SQL/statement/verbs/explain/plan_table/columns/qblock_name) in the [`plan_table`](https://renenyffenegger.ch/notes/development/databases/Oracle/SQL/statement/verbs/explain/plan_table/index) |
| Statement    | entire [SQL statements](https://renenyffenegger.ch/notes/development/databases/Oracle/SQL/statement/index)           | `all_rows`                                                                                                     | Note that `use_nl(tab_a tab_b)` is shortcut for `use_nl(tab_a) use_nl(tab_b)` and therefore is not considered to be a multi-table hint.                                                                                                                                                             | 

## Specifying table names in hints

If a single or multi-table hint refers to a [table](https://renenyffenegger.ch/notes/development/databases/Oracle/objects/tables/index) that is [aliased](https://renenyffenegger.ch/notes/development/databases/Oracle/SQL/select/from/alias/index), the alias needs to be specified in the hint.

Wrong:
```sql
select /*+ index(scott.emp ix_emp) */ from scott.emp  e;
```

Better:
```sql
select /*+ index(e) */ from scott.emp  e;
```

Schema names should be omitted.

## When hints might be used

With an ideal optimizer, hints should not be used. However, it turns out that the optimizer sometimes creates a suboptimal plan in which case better performance can be achieved by hinting the SQL statement.

Sometimes, the characteristics of the selected data changes rapidly so that the relevant [statistics](https://renenyffenegger.ch/notes/development/databases/Oracle/optimizer/statistics/index) are inaccurate which also might lead to a bad plan.

## Jonathan Lewis' list of the Big Five Hints

Jonathan Lewis' list of the [Big Five Hints](https://jonathanlewis.wordpress.com/2015/12/03/five-hints) is:
- [merge](https://renenyffenegger.ch/notes/development/databases/Oracle/SQL/hints/list/merge/index), no_merge
- [push_pred](https://renenyffenegger.ch/notes/development/databases/Oracle/SQL/hints/list/push/pred/index), no_push_pred
- unnest, [no_unnest](https://renenyffenegger.ch/notes/development/databases/Oracle/SQL/hints/list/unnest/no/index)
- push_subq, no_push_subq
- [driving_site](https://renenyffenegger.ch/notes/development/databases/Oracle/SQL/hints/list/driving_site)

## Verifying if hints are correctly specified

Incorrectly specified hints (for example because of a typo) are silently ignored by the optimizer.
In order to verify if all hints are correct and understood by the optimizer, the «flag» `+hint_report` of [dbms_xplan.display](https://renenyffenegger.ch/notes/development/databases/Oracle/installed/packages/dbms/xplan/api/display/index) can be used:
```sql
[explain plan](https://renenyffenegger.ch/notes/development/databases/Oracle/SQL/statement/verbs/explain/index) for
select /*+ no_such_hint */ 42 as num from dual;
```

The following statement reports the erroneous hint at the bottom of the result set with the `E` flag:
```sql
select * from table(dbms_xplan.display(format => '+hint_report'))
  …
   E -  no_such_hint
```

## Global Hints

### Not working for ANSI joins

Oracle's documentation has the following [note](https://docs.oracle.com/en/database/oracle/oracle-database/21/sqlrf/Comments.html#GUID-D316D545-89E2-4D54-977F-FC97815CD62E):

> Specifying a global hint using the _tablespec_ clause does not work for queries that use [ANSI joins](https://renenyffenegger.ch/notes/development/databases/Oracle/SQL/join/ANSI/index), because the optimizer generates additional views during parsing. Instead, specify @queryblock to indicate the query block to which the hint applies.

## See also

An optimizer hint is not to be confused with [SQLcl and SQL Developer select hints](https://renenyffenegger.ch/notes/development/databases/Oracle/SQLcl/index#sqlcl-sqldev-select-hints).

[`v$sql_hint`](https://renenyffenegger.ch/notes/development/databases/Oracle/installed/dynamic-performance-views/sql/hint/index), which can be [joined to `v$sql_feature_hierarchy`](https://renenyffenegger.ch/notes/development/databases/Oracle/installed/dynamic-performance-views/sql/hint/join-feature-hierarchy) to display each hint with an «SQL feature hierarchy» (See [`v$sql_feature_hierarchy`](https://renenyffenegger.ch/notes/development/databases/Oracle/installed/dynamic-performance-views/sql/feature/hierarchy/index)).

The [qb_name](https://renenyffenegger.ch/notes/development/databases/Oracle/SQL/hints/list/qb_name/index) hint specifies the value with which the column [`qblock_name`](https://renenyffenegger.ch/notes/development/databases/Oracle/SQL/statement/verbs/explain/plan_table/columns/qblock_name) in the [`plan_table`](https://renenyffenegger.ch/notes/development/databases/Oracle/SQL/statement/verbs/explain/plan_table/index) is filled.

If the [init parameters](https://renenyffenegger.ch/notes/development/databases/Oracle/adminstration/init-parameters/index) `optimizer_ignore_hints` or `optimizer_ignore_parallel_hints` are set to `true`, ([optimizer](https://renenyffenegger.ch/notes/development/databases/Oracle/optimizer/index) related? and) parallel execution related) hints will be ignored.

Erroneous hints are recorded in the column [`other_xml`](https://renenyffenegger.ch/notes/development/databases/Oracle/SQL/statement/verbs/explain/plan_table/columns/other_xml/index) of the [plan table](https://renenyffenegger.ch/notes/development/databases/Oracle/SQL/statement/verbs/explain/plan_table/index) after executing [`explain plan`](https://renenyffenegger.ch/notes/development/databases/Oracle/SQL/statement/verbs/explain/index) on a an [SQL statement](https://renenyffenegger.ch/notes/development/databases/Oracle/SQL/statement/index).