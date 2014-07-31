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

-default
-unigue:true ( unix index )
-sparse:true - for unix fields that are not in every field
-geospatial
-TTL(time to live) 
-text

```
//Not good
db.sentencees.find({words: "/rat/"}) //can use reqular expressions
//Better
db.sentenc.ensureIndex( { words : "text"})
//indexes all words like multikey in arrays
db.sentenc.find({ $text: { $search: "cat"}})-Text
```