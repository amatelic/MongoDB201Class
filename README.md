MongoDB201Class
===============

M102: MongoDB for DBAs

In this repository we will have some basic examples how to use the mongodb database.

##Basic searching in mongoDB
```node
db.collection.find(<criteria>,<projection>)
```

##Basic searching in with operators

```node
db.collection.find({ number : { $lt: 13 } })
```

comands		  | full name
------------- | -------------
$gt           | greater than
$lt 		  | lover than
$where        | where
$in 		  | equal
$ne 		  | not equal
$nin          | do not exsist

##For serching and sorting 

```
db.collection.find().sort({page : 1}) 
//Or you can
db.collection.find({$query: {}, $orderby: { age: -1 }}) 
```
 1 -> ascending order
-1 -> desending order

##Adding limits

```
db.collection.find().limit( 5 )
```

##Basic concep of indexing in mongo db

How to create an index

db.parts.ensureIndex({ page: 1})

ensureIndex -> create index if it dosen't exsist


##Notes on indexes 

- keys can be any type
- _id index is automatic(unic)
- other than _id, explicity declared
- automaticaly used
- can index array contant(multi keys)
- can index nested subdocuments and subfields
- fielsname are not in the indexes

##Index types

- default
- unigue:true ( unix index )
- sparse:true - for unix fields that are not in every field
- geospatial
- TTL(time to live) 
- text

```
//Not good
db.sentencees.find({words: "/rat/"}) //can use reqular expressions
//Better
db.sentenc.ensureIndex( { words : "text"})
//indexes all words like multikey in arrays
db.sentenc.find({ $text: { $search: "cat"}})-Text
```

##if you have multiple file with the same value
```
db.collection.ensureIndex({ x: 1},{ unique: true, dropDups: true})
delets all data just one stays
```
##Covered indexes
- explain() -> runs the query and outputs witch  index was used
- hint({x:1})->choose witch index to use

``` 
db.collection.fnd().hint({x:1}).explain()
$natural -> force table scann
```

##Reads vs writes performnac on more indexses
- insert <- slower
- update <- situational
- delete <- situational

indexses speed up reads and slow down writes
-moves to other location are expensive because first we have to move tde data to a location whit bigger place and second all indexses have to be changed
*move is expensive if you have a lot of index
-add padiing with compact command
-or make padding more


##Basic procesess

- exercise care killing write op on secondary

- exercise care killing compact

- don't kill interal ops

###Basic operation searching  and destroying

```
db.currentOp();
db.killOp();
```
###Mongo profile

```
command show profile
db.collection.setProfilingLevel()
```
0 = off
1 = select
2 = on 


###Commands for administrator

mongostat
mongotop

###Replication - copies or backup

-"HA" -> high available
- data safety
-"DR" -> disaster recovery

//Replica with sharding?
-replica same daata on diferent servers
-sharding  difernet file// more shard more replication

Replication: 
- is asynchronous
- single primary
-multiple slaves


// Replication
A replication set in MongoDB is a group of mongodb proccess that maintaine the same data set. Replica set provides redundamncy and high availabilitym and are the basis for all production deployment.

Link:http://docs.mongodb.org/manual/replication/
How to create

```
mongod --replSet <arg> //name of the replica set
mongodb ---replSet abc --dbpath 1 --port 27001 --oplogSize 50 --logpath log.1 --logappend --fork

ps --check if mongo is running
db.isMaster()

//initialiy that set
//1.specify configuration
//2.initial data

//creating replica set

var cfg = {
	_id : "abc",
	member: [
	{_id: 0, host:"localhost:27001"	},
	{_id: 1, host:"localhost:27002"	},
	{_id:2, host:"localhost:27003"	}
	]
}

rs.initiate(cfg);

rs.status() //status of servers
```

###best practice
-don't use raw ip address
-don't use names form 
	/etc/hosts
-use DNS 
	-pick an appropriate TTL