---
YamlDesc: CONTENT-ARTICLE
Title: mongodb database
MetaDescription: mongodb, database, create database, drop database
MetaKeywords: mongodb, database, create database, drop database
Author: Venkata Bhattaram / tinitiate.com
ContentName: mongodb-database
---

# MongoDB Database
* In MongoDB `Database` has collections or Tables, and Rows are called as 
  `documents`.
* The Column and Values are Keys and Values.
* Multiple databases can run on a single instance of MongoDB server. 
* MongoDB provides a default database called `db`, It is stored in the data folder.
* In MongoDB Databases can be created on the fly without having to have a 
  database created to begin with.

## Creating a MongoDB Database
* Use the `mongo` at shell or commandline ( in windows ), to enter the 
  `mongo` shell

## MongoDB Commands

## Data Base Commands
* Create Database
```
use database-name
```
* A Database is not created unless a Collection is not in it
* Syntax to create a collection
```
db.createCollection("test")
```

* List all Databases
```
show dbs
```
## Drop Database
* First go to the target database, using the `use data-base` command
* Then issue the `db.dropDatabase()` command
```
use my-database
db.dropDatabase()
```

