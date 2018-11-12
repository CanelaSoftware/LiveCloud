# command cdb_updateTableSchemaMode pTable, pSchemaless
---
## Summary
This command changes the schema mode of tables.

## Inputs
* **pTable** *(String)* - The name of the specified table ID or table name.
* **pSchemaless** *(Bool)* - Determines whether table is schemaless or not.

## Additional Requirements
This API call requires internet access.

## Examples
```
local tTable, tSchemaless

put "clients" into tTable
put true into tSchemaless

cdb_updateTableSchemaMode(tTable,tSchemaless)
```