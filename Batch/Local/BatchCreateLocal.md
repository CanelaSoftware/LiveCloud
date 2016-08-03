# cdb_batchCreateLocal
---
```
function cdb_batchCreateLocal(tInputA)
```
## Summary:
This function stores data locally to one or more tables in a single call. A cdbRecordID is returned for every new record created.

## Inputs:
* **`tInputA`** *(Array)* - A multidimensional array of keys, where each key is a table UUID to another array of keys. This table UUID can be obtained by calling the function *cdb_getTableID* and passing in the table name, returns the table's unique UUID. There must be at least one table UUID key in the array.
    * `[`*`tableID 1`*`]` *(String)* - key that is the first table's UUID, which maps to another array of arbitrary recordKeys, where each recordKey maps to a record. There must be at least one record key in this sub-array.
    	* `[`*`recordKey 1`*`]` *(String)* - An arbritrary user-defined key for a record. Recommended keys are 1, 2, ..., N, where N is the number of stored records in the table with a UUID of *tableID 1*. This recordKey maps to a sub-array of keyNames that map to the actual data to store in a record. There must be at least one keyname in this sub array. 
    		* `[`*`keyName 1`*`]` *(String)* - User-defined keyname, where *keyName 1* is an arbitrary key name. Each keyname maps to the actual user data to store. User must provide at least one key per stored value.
    			*  `yourData` *(String)* - the actual data the user wants to store in this keyname in this record in this table.
    		* `*[`*`keyName N`*`]` *(String)* - The nth user-defined keyname. Repeat *keyName 1*'s sublevel structure.
    	* `*[`*`recordKey N`*`]` *(String)* - the the nth record key. Repeat *recordKey 1*'s sublevel structure.
    * `*[`*`tableID N`*`]` *(String)* - key that is the nth table's UUID. Repeat *tableID 1*'s sublevel structure.

> _*optional parameter._

![BatchCreate input diagram](../../chartimages/createInput.png)
## Outputs:
(Array) -- This output array has similar structure to the input array, except that the recordKeys in the input array are replaced with the corresponding cdbRecordID keys that are associated with the data that the recordKeys contained. The corresponding cdbRecordID keys have empty contents. 

![BatchCreate output diagram](../../chartimages/createOutput.png)
## API Version:
* `0.3.1` - Introduced

## Examples:
```
local tInputA, tTableID, tDataA
     
put cdb_getTableID("clients") into tTableID
          
put fld "firstName" into tInputA[tTableID][1]["firstName"]
put fld "lastName" into tInputA[tTableID][1]["lastName"]
put fld "age" into tInputA[tTableID][1]["age"]
put fld "income" into tInputA[tTableID][1]["income"]

put fld "firstName2" into tInputA[tTableID][2]["firstName"]
put fld "lastName2" into tInputA[tTableID][2]["lastName"]
put fld "age2" into tInputA[tTableID][2]["age"]
put fld "income2" into tInputA[tTableID][2]["income"]

put cdb_batchCreateLocal(tInputA) into tDataA
```