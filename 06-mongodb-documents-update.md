---
YamlDesc: CONTENT-ARTICLE
Title: mongodb collections update
MetaDescription: mongodb, collections,documents update
MetaKeywords: mongodb, collections,documents update
Author: Venkata Bhattaram / tinitiate.com
ContentName: mongodb-documents-update
---

# MongoDB Documents 
* A Collection is like an Database Table
* The Rows are called as **Documents** or Objects
* The Column and Column Values are stored as Key-Values

## MongoDB Updating Documents in a Collection
* Here demonstrate updates to an existing collection
* The update() method updates the values in the existing document 
```
use EmployeeDB
db.Employee.find()
db.Employee.update({'empno':7566},{$set:{'salary':10000}})
db.Employee.find()
```
* Using update() method to update multiple rows, This is done using the 
  **multi** clause
```
db.Employee.update({},{$set:{'Notes':'Employe Data'}},{multi:true})
db.Employee.find()
```

* `save()` method replaces the existing document with the new document passed
  in `save()` method.
```
db.Employee.save({ "_id" : ObjectId("5c75e83d3e777bf70102604f"), "empno" : 7566, "name" : "JONES", "job" : "MANAGER", "boss" : 7839, "hiredate" : ISODate("2014-03-12T18:12:00Z"), "salary" : 5000, "deptno" : 20, "Notes" : "Employee Data" })
db.Employee.find()
```
 