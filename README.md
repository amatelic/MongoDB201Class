MongoDB201Class
===============

M102: MongoDB for DBAs

In this repository we will have some basic examples how to use the mongodb database.

##Basic searching in mongoDB
```node
db.collection.find(<criteria>,<projection>)
```


|Parameter|Type|Description|
----------------------------
|criteria|document|	Optional. Specifies selection criteria using query operators. To return all documents in a collection, omit this parameter or pass an empty document ({})|
|projection|document|Optional. Specifies the fields to return using projection operators. To return all fields in the matching document, omit this parameter.|
