# CloudRecordCount
---
```
function cdb_cloudRecordCount(pTableName)
```
## Summary:
This function counts the number of cloud records in a given database.

## Inputs:
* **`pTableName`** *(String)* - The label of the database to access.

## Outputs:
(String) – Contains the numeric count of records in the cloud.

## API Version:
* `0.3.1` - Introduced

## Examples:
```
local tCount

put cdb_cloudRecordCount("clients") into tCount
```