---
YamlDesc: CONTENT-ARTICLE
Title: mongodb collections
MetaDescription: mongodb, collections, json schema, $jsonSchema, modeling
MetaKeywords: mongodb, collections, json schema, $jsonSchema, modeling
Author: Venkata Bhattaram / tinitiate.com
ContentName: mongodb-collections-json-schema
---

# MongoDB Collections JSON Schema Modeling
* Starting from Mongo 3.6, JSON Schema validation was supported.
* JSON Schema validation enforces datatypes, min max values, on the documents rows.
* This is enforced using the $jsonSchema keyword with the db.createCollection.
* The schema is itself has a JSON document structure.
* All MongoDB Document column datatypes are based on `BSON` This is binary
  serialization format of JSON.

## MongoDB Collection with JSON Schema
* Common MongoDB BSON Datatypes
  * **number**
  * **int**   `32-bit integer` use NumberInt(12345) when inserting
  * **long**  `64-bit integer`
  * **timestamp** `This is the UNIX EPOCH Time Stamp`
  * **date** `Date`
  * **double**
  * **decimal** Use NumberDecimal(100.99) when inserting
  * **string**
  * **bool** `Boolean True/False`
  * **null** `Null is no data (Its not ZERO or SPACE)`
  * **objectId**  `Reference to the Hex ID that Mongo Generates for ID columns`
>
* Here we demonstrate a simple JSON Schema with the basic datatypes
* The Columns or Fields and their data types
 * EmpID - `long`
 * EmpName - `string`
 * JoinDate - `date`
 * Salary - `decimal`
 * CreatedOn - `timestamp` 
```
db.createCollection( "SimpleEmp" , { 
   validator: { $jsonSchema: { 
      bsonType: "object", 
      properties: { 
         EmpID: { 
            bsonType: "number", 
            description: "required and must be a number" }, 
         EmpName: { 
            bsonType: "string", 
            description: "required and must be a string" }, 
         JoinDate: { 
            bsonType: "date", 
            description: "required and must be a date" }, 
         Salary: { 
            bsonType: "double", 
            description: "Enter a $ value" }, 
         CreatedOn: { 
            bsonType: "timestamp", 
            description: "Date and Time when this row was created" }
      }
   }
}
})

//validationAction: "warn"  --- validationAction is warn, MongoDB logs any violations but allows the insertion or update to proceed.
```

* Get Validation Information on the Collection
```
db.getCollectionInfos({name:"SimpleEmp"})[0].options.validator
```
* Drop Collection
```
db.SimpleEmp.drop()
```

* Insert values
```
db.SimpleEmp.insert({EmpID : 3, EmpName : "XYZ", JoinDate : new Date(2014, 11, 12, 14, 12), Salary : 10000.20, CreatedOn : new Timestamp(1412180887,1) })
db.SimpleEmp.insert({EmpID : 3, EmpName : "XYZ", JoinDate : new Date(2014, 11, 12, 14, 12), CreatedOn : new Timestamp(1412180887,1) })
```

## MongoDB Validator Applying Check Constraints on Column Values
* Mongo JSON Schema Validator also supports the following constraints to be 
  enforced on the columns
  * Enforce Mandatory Column values using `required` clause
  * Enforce List of values for column values with `enum` clause
  * Enforce data patterns with regular expressions Using `pattern` clause
  * Enforce MIN and MAX values using `minimum` and `maximum`
* `ValidationAction` clause directs MongoDB as to how to handle documents 
  that violate the validation rules, `error` is the default, it could be set 
  to `warn`.
```
db.createCollection( "person" , {
    validator: { $jsonSchema: {
        bsonType: "object",
        required: [ "name", "email" ],
        properties: {
        name: {
            bsonType: "string" },
        email: {
            bsonType: "string",
            pattern: "^.+\@.+$" },
        year_of_birth: {
            bsonType: "int",
            minimum: 1900,
            maximum: 2001,
            description: "the value must be between 1900 and 2001" },
        gender: {
            enum: [ "M", "F" ],
            description: "Must be M or F" }
        }
    }},
    validationAction: "warn"
})
```

## Mongo DB Complex BSON data types
* Object
* Array
* Binary Data
* DBPointer
