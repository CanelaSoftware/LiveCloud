# cdb_lookUpLocalValue
---
```
function cdb_lookUpLocalValue tInputA
```
## Summary:
This function returns the value associated with a given key for a given local record.

## Inputs:
* **`tInputA`** *(Array)* - An array of keys containing data per the following format:
    * `["cdbTableName"]` *(String)* - The specified table name.
    * `["cdbRecordID"]` *(String)* - The record ID of the specified record.
    * `["key"]` *(String)* - The key to retrieve.

## Outputs:
*(String)* – Contains the value of the given key for the specified record.

## API Version:
* `0.3.1` - Introduced

## Examples:
```
local tInputA 

put fld "workingTableName data" into tInputA["cdbTableName"]
put line 1 of fld "recordID data" into tInputA["cdbRecordID"]
put "firstName" into tInputA["key"]
     
put cdb_lookUpLocalValue(tInputA) into tValue
```