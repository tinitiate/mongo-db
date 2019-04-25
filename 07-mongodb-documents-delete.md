---
YamlDesc: CONTENT-ARTICLE
Title: mongodb collections delete
MetaDescription: mongodb, collections,documents delete
MetaKeywords: mongodb, collections,documents delete
Author: Venkata Bhattaram / tinitiate.com
ContentName: mongodb-documents-delete
---

# MongoDB Documents 
* A Collection is like an Database Table
* The Rows are called as **Documents** or Objects
* The Column and Column Values are stored as Key-Values

## MongoDB Deleting Documents in a Collection
* Here demonstrate delete documents from an existing collection
* The remove() method deletes the values in the existing document 
* Remove All documents matching condition from a collection
```
use EmployeeDB

// Before Remove
db.Emp.find()

// Remove Data by document column name
db.Emp.remove({'EmpID':3})

// After Remove
db.Emp.find()
```
* Remove single document matching condition from a collection
```
use EmployeeDB

// Before Remove
db.Emp.find()

// Remove Data by document column name, use the (COMMA,1)
db.Emp.remove({'EmpID':3},1)

// After Remove
db.Emp.find()
```
* Remove all using the .remove({})
```
db.Emp.remove({})
```
