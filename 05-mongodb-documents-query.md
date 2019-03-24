---
YamlDesc: CONTENT-ARTICLE
Title: mongodb collections query
MetaDescription: mongodb, collections,documents query
MetaKeywords: mongodb, collections,documents query
Author: Venkata Bhattaram / tinitiate.com
ContentName: mongodb-documents-query
---

# MongoDB Querying Documents 
* A Collection is like an Database Table
* The Rows are called as **Documents** or Objects
* The Column and Column Values are stored as Key-Values

## Setup Test Collections for Document Query Tutorial
* Here demonstrate various features of Document Query, We create THREE 
  Collections with schema and relationships.
* Create Collection `Employee` in a database called `EmployeeDB`
```
// Create Documents in DBEmpDept Database
use DBEmpDept

// Create the Department Collection
db.createCollection( "Department" , { 
   validator: { $jsonSchema: { 
      bsonType: "object", 
      properties: { 
         deptno: { 
            bsonType: "number", 
            description: "The Dept ID" }, 
         name: { 
            bsonType: "string", 
            description: "Department Name" }, 
         location: { 
            bsonType: "string", 
            description: "Department Location" }
      }
   }
}
})

// Insert into Department Collection
db.Department.insert(
   [
     { deptno : 10, name : "ACCOUNTING", location: "NEW YORK"}
    ,{ deptno : 20, name : "RESEARCH", location: "DALLAS"}
    ,{ deptno : 30, name : "SALES", location: "CHICAGO"}
    ,{ deptno : 40, name : "OPERATIONS", location: "BOSTON"}
   ]
);

// Create the Employee Collection
db.createCollection( "Employee" , { 
   validator: { $jsonSchema: { 
      bsonType: "object", 
      properties: { 
         empno: { 
            bsonType: "number", 
            description: "The Employee ID" }, 
         name: { 
            bsonType: "string", 
            description: "Employee Name" }, 
         job: { 
            bsonType: "string", 
            description: "Job Role" }, 
         boss: { 
            bsonType: "number", 
            description: "Boss EmpNO" }, 
         hiredate: { 
            bsonType: "date", 
            description: "Join Date" }, 
         salary: { 
            bsonType: "double", 
            description: "Emp Salary" }, 
         comm: { 
            bsonType: "double", 
            description: "Commission" }, 
         deptno: { 
            bsonType: "number", 
            description: "Department Number Foreign Key to the Department Collection" }
      }
   }
}
})

// Insert into Employee Collection
db.Employee.insert (
   [
        {empno: 7839, name: "KING",   job: "PRESIDENT",             hiredate:  new Date(2014, 1, 12, 14, 12),   salary: 5000,             deptno: 10}
       ,{empno: 7566, name: "JONES",  job: "MANAGER",   boss: 7839, hiredate:  new Date(2014, 2, 12, 14, 12),   salary: 2975,             deptno: 20}
       ,{empno: 7788, name: "SCOTT",  job: "ANALYST",   boss: 7566, hiredate:  new Date(2012, 11, 12, 14, 12),  salary: 3000,             deptno: 40}
       ,{empno: 7876, name: "ADAMS",  job: "CLERK",     boss: 7788, hiredate:  new Date(2011, 6, 12, 14, 12),   salary: 1100,             deptno: 20}
       ,{empno: 7902, name: "FORD",   job: "ANALYST",   boss: 7566, hiredate:  new Date(2012, 10, 12, 14, 12),  salary: 3000,             deptno: 40}
       ,{empno: 7369, name: "SMITH",  job: "CLERK",     boss: 7902, hiredate:  new Date(2016, 8, 12, 14, 12),   salary: 800,              deptno: 40}
       ,{empno: 7698, name: "BLAKE",  job: "MANAGER",   boss: 7839, hiredate:  new Date(2011, 7, 12, 14, 12),   salary: 2850,             deptno: 30}
       ,{empno: 7499, name: "ALLEN",  job: "SALESMAN",  boss: 7698, hiredate:  new Date(2012, 6, 12, 14, 12),   salary: 1600, comm: 1400            }
       ,{empno: 7521, name: "WARD",   job: "SALESMAN",  boss: 7698, hiredate:  new Date(2014, 4, 12, 14, 12),   salary: 1250,             deptno: 30}
       ,{empno: 7654, name: "MARTIN", job: "SALESMAN",  boss: 7698, hiredate:  new Date(2013, 12, 12, 14, 12),  salary: 1250, comm: 1400, deptno: 30}
       ,{empno: 7844, name: "TURNER", job: "SALESMAN",  boss: 7698, hiredate:  new Date(2012, 11, 12, 14, 12),  salary: 1500, comm:    0, deptno: 30}
       ,{empno: 7900, name: "JAMES",  job: "CLERK",     boss: 7698, hiredate:  new Date(2011, 2, 12, 14, 12),   salary: 950,              deptno: 30}
       ,{empno: 7782, name: "CLARK",  job: "MANAGER",   boss: 7839, hiredate:  new Date(2011, 1, 12, 14, 12),   salary: 2450,             deptno: 10}
       ,{empno: 7934, name: "MILLER", job: "CLERK",     boss: 7782, hiredate:  new Date(2014, 01, 12, 14, 12),  salary: 1300}
   ]
);
```

### Simple join / filter conditions 
* Query all documents in a collection
```
db.Department.find({})
```
* Equality	{<key>:<value>}	find by value equal to
* Query by Field Value, Here we `find()` all documents where job = "SALESMAN"
```
db.Employee.find( { job: "SALESMAN" } )
```
* Less Than	{<key>:{$lt:<value>}} find by value Less Than
* Query by Field Value, Here we `find()` all documents where salary < 2000
```
db.Employee.find( { salary: {$lt:2000 } } )
```
* Less Than Equals {<key>:{$lte:<value>}}, find by value Less Than or equal to
* Query by Field Value, Here we `find()` all documents where salary < 2000
```
db.Employee.find( { salary: {$lte:2000 } } )
```
* Greater Than {<key>:{$gt:<value>}}, find by value Greater Than
* Query by Field Value, Here we `find()` all documents where salary < 2000
```
db.Employee.find( { salary: {$gt:2000 } } )
```
* Greater Than Equals	{<key>:{$gte:<value>}}, find by value Greater Than or equal to
* Query by Field Value, Here we `find()` all documents where salary < 2000
```
db.Employee.find( { salary: {$gte:2000 } } )
```
* Not Equals {<key>:{$ne:<value>}}, find by value not equal given value
* Query by Field Value, Here we `find()` all documents where job != "SALESMAN"
```
db.Employee.find( { job: {$ne:"SALESMAN" } } )
```


### Querying Fields by Value
* Select Specified Fields (_id Field is also selected)
  * Same as `select name,salary from Employee where job = 'SALESMAN';
```
db.Employee.find( { job: "SALESMAN"}, { name: 1, salary: 1 } )
```
* Ignore _id Field from the above query
```
db.Employee.find( { job: "SALESMAN"}, { name: 1, salary: 1, _id:0} )
```
* Return All But the Excluded Fields
```
db.Employee.find( { job: "SALESMAN" }, { salary: 0 } )
```

### Querying with AND condition
* AND condition gets data based on TWO qualifying filter conditions
* db.mycol.find({ $and: [{key1: value1}, {key2:value2}]}
* Here we get all data from Employee, where salary>2000 and job not equal to "SALESMAN"
```
db.Employee.find( {$and:[{ salary: {$gte:2000 }}, {job: {$ne:"SALESMAN" } }]} )
```

### Querying with OR condition
* OR condition gets data based any one of the TWO qualifying filter conditions
* db.mycol.find({ $or: [{key1: value1}, {key2:value2}]}
* Here we get all data from Employee, where salary>2000 or job is "SALESMAN"
```
db.Employee.find( {$or:[{ salary: {$gte:2000 }}, {job:"SALESMAN" }]} )
```

### Querying with both AND and OR condition
* Get all data where job='salesman' and (sal <= 200 or deptno=20)
```
db.Employee.find({"job": "SALESMAN", $or: [{"salary": {$lte:2000 }},{"deptno": 20}]})
```

### Querying Null Values
* List all field values that are null
```
db.Employee.find( { boss: null } )
```
* Find Null values using Existence Check
```
db.Employee.find( { boss : { $exists: false } } )
```


### Query Sort() and Limit()
* `Sort()` 
* Sort data in Ascending Order use column name and 1
* Sort data in Descending Order use column name and -1
```
db.Employee.find().sort({empno:-1})
db.Employee.find().sort({empno:1})
```
* Sort by multiple columns
```
db.Employee.find().sort({job:1, name:1})
```
* `Limit()` 
* Limit rows to be selected using the limit function
* Here we limit the data after retrieving the first 2 rows
```
db.Employee.find().limit(2);
```


### Query count()
* `count()` 
* Counts the JSON Rows
```
db.Employee.find().count()
```


### Query pretty()
* `pretty()` 
* Prettifies the JSON output
```
db.Employee.find().sort({empno:-1}).pretty()
```



