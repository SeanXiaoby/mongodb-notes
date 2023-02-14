# MongoDB - Study Notes
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
  - [Documents level]()

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

### Access databases' meta data

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

### Database level

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

### Collection level

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

### Documents level
