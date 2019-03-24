---
YamlDesc: CONTENT-ARTICLE
Title: mongodb collections insert
MetaDescription: mongodb, collections,documents insert
MetaKeywords: mongodb, collections,documents insert
Author: Venkata Bhattaram / tinitiate.com
ContentName: mongodb-documents-insert
---

# MongoDB Documents 
* A Collection is like an Database Table
* The Rows are called as **Documents** or Objects
* The Column and Column Values are stored as Key-Values

## MongoDB Inserting Documents into a Collection
* Here demonstrate
* Create Collection `Employee` in a database called `EmployeeDB`
```
use EmployeeDB
db.createCollection( "Emp" , { 
    validator:
      { $jsonSchema: { 
        bsonType: "object", 
        properties: { 
           EmpID: { bsonType: "number"}, 
           EmpName: { bsonType: "string"}, 
           JoinDate: { bsonType: "date"}, 
           Salary: { bsonType: "double"}, 
           CreatedOn: { bsonType: "timestamp"}
      }
   }
}
})
```

* Insert One Document to the Collection in a single statement
```
db.Emp.insert({EmpID : 3, EmpName : "XYZ", JoinDate : new Date(2014, 11, 12, 14, 12), Salary : 10000.20, CreatedOn : new Timestamp(1412180887,1) })
```

* Insert Many Document to the Collection in a single statement
```
db.Emp.insert(
   [
     {EmpID : 11, EmpName : "AAA", JoinDate : new Date(2014, 11, 12, 14, 12), Salary : 10000.50, CreatedOn : new Timestamp(1412180887,1) }
    ,{EmpID : 22, EmpName : "BBB", JoinDate : new Date(2014, 11, 12, 14, 12), Salary : 10000.50, CreatedOn : new Timestamp(1412180887,1) }
    ,{EmpID : 33, EmpName : "CCC", JoinDate : new Date(2014, 11, 12, 14, 12), Salary : 10000.50, CreatedOn : new Timestamp(1412180887,1) }
   ]
);
```

* Insert Documents with db.COLLECTION.save()
```
db.Emp.save({EmpID : 55, EmpName : "XYZ", JoinDate : new Date(2014, 11, 12, 14, 12), Salary : 10000.20, CreatedOn : new Timestamp(1412180887,1) })
```


* List all the documents from the collection
```
db.Emp.find()
```
