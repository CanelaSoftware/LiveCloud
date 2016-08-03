# cdb_batchUpdateCloud
---
```
command cdb_batchUpdateCloud tInputA
```
## Summary:
This command makes changes to a number of records on the cloud, without making changes to the corresponding local records.

## Inputs:
* **`tInputA`** *(Array)* - A multidimensional array of keys, where each key is a table UUID that maps to another array of keys. This table UUID can be obtained by calling the function *cdb_getTableID* and passing in the table name, returns the table's unique UUID. There must be at least one table UUID key in this array.
    * `[`*`tableID 1`*`]` *(String)* - key that is the first table's UUID, which maps to another array of arbitrary record keys. There must be at least one record key in this sub-array.
    	* `[`*`recordKey 1`*`]` *(String)* - An arbritrary user-defined key for a record. Recommended keys are 1, 2, ..., N, where N is the number of stored records in the table with a UUID of *tableID 1*. Each recordKey maps to a sub-array of keys where each key is a key for the actual data to store in a record. There must be at least one key name in this sub array. 
    		* `[`*`keyName 1`*`]` *(String)* - User-defined keyname, where *keyName 1* is an arbitrary key name. Each keyname maps to the actual user data to update. User must provide at least one self-defined keyname.
    			*  `yourData` *(String)* - the actual data the user wants to update in this keyname in this record in this table.
    		* `*[`*`keyName N`*`]` *(String)* - The nth user-defined keyname. Repeat *keyName 1*'s sublevel structure.
    	* `*[`*`recordKey N`*`]` *(String)* - The nth record key. Repeat *recordKey 1*'s sublevel structure.
    * `*[`*`tableID N`*`]` *(String)* - key that is the nth table's UUID. Repeat *tableID 1*'s sublevel structure.

> _*optional parameter._

> Note: for each record, one of its keyNames must be "cdbRecordID" and it must contain the record ID for that record to be updated.

![BatchUpdate input diagram](../../chartimages/updateInput.png)
## Additional Requirements:
This API call requires internet access.
## API Version:
* `0.3.1` - Introduced

## Examples:
```
local tInputA, tTableID
     
put cdb_getTableID("clients") into tTableID
          
put fld "firstName" into tInputA[tTableID][1]["firstName"]
put fld "lastName" into tInputA[tTableID][1]["lastName"]
put fld "age" into tInputA[tTableID][1]["age"]
put fld "income" into tInputA[tTableID][1]["income"]

put fld "firstName2" into tInputA[tTableID][2]["firstName"]
put fld "lastName2" into tInputA[tTableID][2]["lastName"]
put fld "age2" into tInputA[tTableID][2]["age"]
put fld "income2" into tInputA[tTableID][2]["income"]

cdb_batchUpdateCloud tInputA
```