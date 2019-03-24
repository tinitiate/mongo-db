---
YamlDesc: CONTENT-ARTICLE
Title: mongodb database
MetaDescription: mongodb, database, create database, drop database
MetaKeywords: mongodb, database, create database, drop database
Author: Venkata Bhattaram / tinitiate.com
ContentName: mongodb-users
---
# MongoDB Users
* MongoDB provides TWO types of users, ADMIN and APPLICATION Users
* 
## Create Admin User
* Create Admin User: mongoadmin
```
use admin
db.createUser({ user: "admin"
               ,pwd: "admin"
               ,roles: [{role:"userAdminAnyDatabase", db: "admin"}]
               })
```
* Exit the shell and use the command at command prompt/shell to Logon to 
  MongoDB using the command at commandline
* Connect to MongoDB as Admin
```
mongo admin -u admin -p admin
```

## Create Application User
* Application User has no Admin roles, but might have Read/Write privileges
```
use emp;
db.createUser({ user: "app_user1", pwd: "app_user1", roles: [{ role: "readWrite", db: "emp" }] })
```


## Change User Roles
* Common Roles of MongoDB
 * `dbAdminAnyDatabase`
 * `readWriteAnyDatabase`
 * `userAdminAnyDatabase`
 * `dbAdmin`
 * `readWrite`
 * `read`
* **Assign New Role to user**
```
use emp;
db.grantRolesToUser(
   "app_user1",
   [ { role : "read", db : "emp" }]
)
```
* Get Roles of a User
```
db.getUser("app_user1")
```
>
* **Revoke Role from User**
```
use emp;
db.revokeRolesFromUser(
   "app_user1",
   [ { role : "read", db : "emp" }]
)
```
 
 
## Delete User
* Delete Application User
```
use emp;
db.runCommand( {
   dropUser: "app_user1",
   writeConcern: { w: "majority", wtimeout: 5000 }
} )
```
