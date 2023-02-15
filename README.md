# [<img src="https://upload.wikimedia.org/wikipedia/commons/9/93/MongoDB_Logo.svg" width = 35%>](https://www.mongodb.com/docs/)
The very tutorial for starters learning MongoDB
- Author: Sean
- Date created: Feb 14<sup>th</sup>, 2023

## Contents
- [MongoDB installation]()
- [MongoDB and NoSql]()
- [MongoDB services]()
- [Basic MongoDB syntax]()
  - [Access databases' meta data]()
  - [Database level]()
  - [Collection level]()
- [Documents CRUD]()

---

## MongoDB Installlation

For various operating systems:

- [Ubuntu]()
- [Docker]()
- [MacOS]()
- [Windows]()

### Ubuntu

Official instructions: [here](https://www.mongodb.com/docs/manual/tutorial/install-mongodb-on-ubuntu/)

```shell
wget -qO - https://www.mongodb.org/static/pgp/server-6.0.asc | sudo apt-key add -

## Here we have to specify Ubuntu version, and we use 16.04 as an example
echo "deb [ arch=amd64,arm64 ] https://repo.mongodb.org/apt/ubuntu xenial/mongodb-org/6.0 multiverse" | sudo tee /etc/apt/sources.list.d/mongodb-org-6.0.list

sudo apt-get update

sudo apt-get install -y mongodb-org
```

### Docker

Official docker image: [here](https://hub.docker.com/_/mongo)

#### Run docker:

```shell
docker run --name some-mongo -d mongo:tag
```
... where ``some-mongo`` is the name you want to assign to your container and ``tag`` is the tag specifying the MongoDB version you want. See the list above for relevant tags.

MongoDB service is initialized when the container is running!

#### Connect to mongoDB via another docker container

```shell
docker run -it --network some-network --rm mongo mongosh --host some-mongo test
```

#### Access MongoDB shell

```shell
docker exec -it some-mongo bash
```

### MacOS

### Windows

---

## MongoDB and NoSql

MongoDB is a source-available cross-platform document-oriented database program. Classified as a NoSQL database program, MongoDB uses JSON-like documents with optional schemas. MongoDB is an NoSql database which is most alike a Sql database.

### Sql vs NoSql

|Aspects|Sql|NoSql|
|---|---|---|
|Data formats|Relational tables with primary keys|Collections and JSON-like documents|
|Difficulty to scale |Hard to scale|Easy to scale|
|Scaling pattern| Scale vertically| Scale horizontally|
|Other characteristics| Data consistensy| Same|

### MongoDB terminology

|Sql| MongoDB| 
|---|---|
|Database| Database|
|Tables|Collections|
|Row| Documents|
|Index|Index|
|Table joins| \ |
|Primary key| Primary key|

---

## MongoDB services

### Start and Stop Mongo service

Start MongoDB service

```shell
sudo service mongod start
```

Stop MongoDB service

```shell
sudo service mongod stop
```

### Access MongoDB shell

```shell
mongosh
```

---

## Basic MongoDB syntax

- ### Access databases' meta data

These are each database' special collection. To access, we can:

```shell
dbname.system.*
```

Options:

|Namespaces| Descriptions|
|---|---|
|dbname.system.namespaces	|List all namespaces|
|dbname.system.indexes	|list all indexes|
|dbname.system.profile	|List database's profile info|
|dbname.system.users	|List all users who can access the database|
|dbname.local.sources	|List slaves' info|

- ### Database level

#### Show all dbs:

```shell
show dbs
```

#### Create/Switch to a specific database:

```shell
use _DB_NAME_
```

**Notes**: 
- The defaulf entry db is ``test``.
- MongoDB will automatically create a db if the ``use``-ed one does not exist.

#### Show current database info

Show current database name:

```shell
db
```

#### Delete current database

```shell
db.dropDatabase()
```

- ### Collection level

#### Create collection

Create a collection:

```shell
db.createCollection(name, options)
```

[Options](https://www.mongodb.com/docs/manual/reference/method/db.createCollection/)

Or we can directly access a collection without creating it ahead(Assume the we choose the collection name ``users``):

```shell
db.users.insertOne({name: "Sean"})
```

Again, MongoDB will automatically create the collection if it does not exist.

#### Show collections

```shell
show collections
## or: show tables
```

#### Delete collections

```shell
db.<collection_name>.drop()
```

---

## Documents CRUD

- ### Documents creation

Insert one:

```shell
db.collection.insertOne({key: value})
```

Insert multiple documents:

```shell
db.collection.insertMany(
   [ <document 1> , <document 2>, ... ],
   {
      writeConcern: <document>,
      ordered: <boolean>
   }
)
```
[Optional parameters](https://www.mongodb.com/docs/manual/reference/method/db.collection.insertMany/)

**Notes**: In MongoDB, each document stored in a collection requires a unique ``_id`` field that acts as a primary key. If an inserted document omits the ``_id`` field, the MongoDB driver automatically generates an ObjectId for the ``_id`` field.

- ### Documents query

#### Select All Documents in a Collection

```shell
db.collection.find({})
```

#### Specify Equality Condition

To specify equality conditions, use ``<field>:<value>`` expressions:
```shell
db.collection.find( { <field1>: <value1>, ... } )
```

Example:

```shell
db.collection.find{ name: "Sean", age: 24 }
```

To only get part of the fields, we use the second parameter in ``find()`` method:

```shell
db.collection.find( { <field1>: <value1>, ... }, { <field1>: boolean, <field2>: boolean,... } )
```

For each field, the boolean indicates if we want this field to be selected.
- If we want this field, we set it to be ``1``
- If we don't want, we set it to be ``0``
- If we don't specify, the field is not selected by default
- ``_id`` is always selected by default unless we specify it to be ``0``

#### Specify Conditions Using Query Operators

Query Operators should be JSON-format:

```shell
{ <Query_operator1>: value,  <Query_operator2>: value, ...} 
```

And we can use Query Operators as values to the keys:

```shell
db.collection.find( { age: { $lt: 30} } )
```

Complete query conditions [here](https://www.mongodb.com/docs/manual/reference/operator/query/)

#### SELECT ``AND`` operator

```shell
db.collection.find( { key1: value1, key2: value2, ...} )
```

#### SELECT ``OR`` operator

```shell
db.collection.find( { $or: [{key1: value1}, {key2: value2}, ...] )
```

---

[Back To top]()







