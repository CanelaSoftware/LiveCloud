# cdb_QueryLocal
---
```
function cdb_QueryLocal(tQueryA)
```
## Summary:
This function searches the specified local table, and returns the subset that matches that query in several possible formats.

## Inputs:
* **`tInputA`**  *(Array)* - An array of keys containing the query, the table name, and an optional output format.
	* `["query"]` *(Array)* - An array formatted as follows:
    	* `["key"]` *(String)* - One of the following:
    		- *`yourKey`* - Searches the specified key
    		- `"$"` - Searches all schema-defined keys
    		- `"*"` - Searches all schema-defined keys and internal keys.
    	* `["value"]` *(String)* - The value to compare against each record's value at the key specified above.
    	* `["operator"]` *(String)* - The comparison operator to compare each record's value at the key specified above to the value specified above. [Click here](../chartimages/QueryOps.png) to see available operators.
    - `["cdbTableName"]` *(String)* - The table name or table ID to search through.
    - `*["resultFormat"]` *(String)* - 
    	-  `"recordList"` *(default)* - returns a line-delimited list of the recordIDs that match the query.
    	- `"recordData"` - returns an array of full records that match the query.

![Query input diagram](../chartimages/QuerySimpleInput.png)

> _*optional parameter._

## Outputs:
* *(String)* - If *pInputA["resultFormat"]* is "recordList" or if no such key is provided:
	* Output is  a line-delimited list of the recordIDs that match the query.
* *(Array)* - If *pInputA["resultFormat"]* is "recordData":
	* Output is an array where each key is a recordID that matches the query, with subkeys defined by the schema.

## API Version:
* `0.3.1` - Introduced

## Examples:
```
local tQueryA, tInputA

put "transactionAmount" into tQueryA["key"]
put "25.00" into tQueryA["value"]
put ">" into tQueryA["operator"]
put tQueryA into tInputA["query"]
put "transactions" into tInputA["cdbTableName"]
get cdb_QueryLocal(tInputA) 
-- list all cdbRecordIDs with 'transactionAmounts' greater than 25.00
```

```
local tInputA

put cdb_BuildQuery("firstName","=","Kevin") into tInputA["query"]
put "users" into tInputA["cdbTableName"]
put "recordData" into tInputA["resultFormat"]
get cdb_QueryLocal(tInputA) 
-- array of all records with firstName 'Kevin' located in the "users" table
```