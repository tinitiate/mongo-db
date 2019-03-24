---
YamlDesc: CONTENT-ARTICLE
Title: mongodb collections
MetaDescription: mongodb, collections, create collection
MetaKeywords: mongodb, database, create collection
Author: Venkata Bhattaram / tinitiate.com
ContentName: mongodb-collections
---

# MongoDB Collections
* A Collection is like an Database Table
* The Rows are called as Documents or Objects
* The Column and Column Values are stored as Key-Values

## MongoDB Create Collection
* Create Collection `Employee` in a database called `EmployeeDB`
```
use EmployeeDB
db.createCollection("Employee")
```
* List all Collections in a Database
```
show collections
```
* Add documents to a collection
* Insert Document to a collection
```
db.Employee.insert({"emp_id":1, "emp_name" : "ABC"})
db.Employee.insert({"emp_id":2, "emp_name" : "PQR"})
db.Employee.insert({"emp_id":3, "emp_name" : "XYZ"})
```
* List all the documents from the collection
```
db.Employee.find()
```

## MongoDB Create Collection With Primary Key
* ObjectID, denoted by the `_id` field of the document is the built-in 
  **PRIMARY KEY** in mongodb.
* Every document after insert will have a key called  `_id`
 by default this is a **12 byte hexadecimal** value 
 for example `"_id" : ObjectId("5c4fcdeb1b95f8d4100aedce"),`
* Consider the system generated Object ID to the user defined in the below example
```
db.Employee.insert({"emp_id":4, "emp_name" : "BBB"})
db.Employee.insert({_id:1,"emp_id":5, "emp_name" : "CCC"})
```
* List all documents in the `Employee` collection
```
db.Employee.find()
```

## MongoDB Drop Collection
* Drop a collection (Remove from MongoDB along with data)
```
db.Employee.drop()
```
