# MongoDB Notes

### MongoDB is a powerful, flexible, and scalable general-purpose document-oriented database. It combines the ability to scale out with features such as secondary indexes, range queries, sorting, aggregations, and geospatial indexes.

- A document-oriented database replaces the concept of a “row” with a more flexible model, the “document” By allowing embedded documents and arrays, the document oriented approach makes it possible to represent complex hierarchical relationships with a  single record

- There are also no predefined schemas: a document’s keys and values are not of fixed types or sizes. Without a fixed schema, adding or removing fields as needed becomes easier

- **Scaling** : MongoDB was designed to scale out. Its document-oriented data model makes it easier for it to split up data across multiple servers.
_MongoDB automatically takes care of_ : 
  - Balancing data and load across a cluster
  - Redistributing documents automatically
  - Routing user requests to the correct machines
  

- When a cluster need more capacity, new machines can be added and MongoDB will figure out how the existing data should be spread to them

## **Key Concepts**

- MongoDB is made up of databases and A database can have zero or more collections
- Collections are made up of zero or more documents. A document is made up of one or more fields and every document has a special field, "_id", that is unique within a collection
- MongoDB comes with a JavaScript shell, which is useful for the administration of MongoDB instances and data manipulation
- Indexes in MongoDB function mostly like their RDBMS counterparts
- MongoDb has **cursors**. when you ask MongoDB for data, it returns a pointer to the result set called a cursor. We can perform various operations like counting or skipping ahead

## **Documents**

- A document is the basic unit of data for MongoDB and is roughly equivalent to a row in a relational database
- A MongoDB document is a group of key and value pairs {someKey1 : someValue1, someKey2 : someValue2 }
- Each key and its value can be thought of as an attribute (field, column) of a document
- The key is always a string and the value can be one of a number of types
- Here is an example of a simple document {"greeting" : "Hello, world!", "foo" : 3}
- MongoDB is type-sensitive and case-sensitive. For example, these documents are distinct:
        {"foo" : 3}
        {"foo" : "3"}

  As are as these:
        {"foo" : 3}
        {"Foo" : 3}
        
- MongoDB document keys are uniques. {"greeting" : "Hello, world!", "greeting" : "Hello, MongoDB!"} is not possible

## **Collections**

- A collection is a group of documents. If a document is the MongoDB analog of some row in a relational database, A collection can be thought of as the analog to a table
- MongoDB collections do not have a **predefined schema**, since documents are self describing

## **Databases**

- In addition to grouping documents by collection, MongoDB groups collections into databases
- A single instance of MongoDB can host several databases, each grouping together zero or more collections
- A database has its own permissions, and each database is stored in separate files on disk

## **MongoDB Shell**

- MongoDB comes with a JavaScript shell that allows interaction from the command line
- To start the shell, run the mongo executable: $ mongo
- MongoDB Shell is a full-featured JavaScript interpreter, capable of running arbitrary JavaScript programs and also a standalone MongoDB client
- **On startup, the shell connects to the test database on a MongoDB serve, and assigns this database connection to the global variable db, which is the primary access point to your MongoDB server through the shell**
- **Inserting and Saving Documents** : Inserts are the basic method for adding data to MongoDB To insert a document into a collection, use the collection’s insert method: db.foo.insert({"bar" : "baz"})
- **Removing Documents** : db.foo.remove() will remove all of the documents in the foo collection. This doesn’t actually remove the collection, and any meta information about it will still exist
- db.mailing.list.remove({"opt-out" : true}) will delete mailing.list collection where the value for "optout“ is true




**Shell Commands**
  - Current databse : db
  - Changing database : use db2
  - Collections can be accessed from db variable : db.abc will return abc collection in the current database
  - Print all items in the cursor: 
        cursor = db.somCollection.find();
        while ( cursor.hasNext() ) { printjson( cursor.next() ); }

 **id and ObjectId**
 - Every document stored in MongoDB must have an "id" key. The "id" key’s value can be any type, but it defaults to an ObjectId
 - In a collection, every document must have a unique value for "id“, Which ensures that every document can be uniquely identified. That is, if you had two collections, each one could have a document where the value for "id" was 123
However, neither collection could contain more than one document with an "id" of 123

## **CRUD Methods**:  **db.[collection].[method]( [filter], [options])**
  
- **db** : current database, **collection** : name of the target collection for method, **method** : desired method, **options** : operation perfromed

### **CREATE** 
- Create or insert operations add new documents to a collection and If the collection does not currently exist, insert operations will create the collection
- Method: db.collection.insertOne() | db.collection.insertMany()
- Example : 
  - db.inventory.insertOne({ item: "canvas", qty: 100, tags: ["cotton"], size: { h: 28, w: 35.5, uom: "cm" } } )
  - db.inventory.insertMany([
               { item: "journal", qty: 25, tags: ["blank", "red"], size: { h: 14, w: 21, uom: "cm" } },
               { item: "mat", qty: 85, tags: ["gray"], size: { h: 27.9, w: 35.5, uom: "cm" } },
               { item: "mousepad", qty: 25, tags: ["gel", "blue"], size: { h: 19, w: 22.85, uom: "cm" }                                       }
            ])

### **READ** 
- Read operations retrieves documents from a collection; i.e. queries a collection for documents: **db.collection.find()**
- To select all documents in the collection pass empty document as query filter parameter: **db.inventory.find({})**
- **Read Methods**
  - $eq : Matches values that are equal to a specified value.
  - $gt : Matches values that are greater than a specified value.
  - $gte : Matches values that are greater than or equal to a specified value.
  - $in : Matches any of the values specified in an array.
  - $lt : Matches values that are less than a specified value.
  - $lte : Matches values that are less than or equal to a specified value.
  - $ne : Matches all values that are not equal to a specified value.
  - $nin : Matches none of the values specified in an array.

### **UPDATE**
- Update operations modify existing documents in a collection
- Methods: 
  - db.collection.updateOne(<filter>, <update>, <options>)
  - db.collection.updateMany(<filter>, <update>, <options>)
  - db.collection.replaceOne(<filter>, <replacement>, <options>)
- Write operations in MongoDB are atomic on the level of a single document
- MongoDb allows to specify criteria, or filters, that identify the documents to update
   - example : db.users.updatemany({age : {$lt : 18 }}, {$set : {status : 'reject'}})
   - Note : $set, will create the field if the field does not exist
- **Update Operators** Fields
   - $currentDate : Sets the value of a field to current date, either as a Date or a Timestamp.
   - $inc : Increments the value of the field by the specified amount.
   - $min : Only updates the field if the specified value is less than the existing field value.
   - $max : Only updates the field if the specified value is greater than the existing field value.
   - $mul : Multiplies the value of the field by the specified amount.
   - $set : Sets the value of a field in a document.
   - $unset : Removes the specified field from a document.
  
- **Update Operators** Arrays
   - $addToSet : Adds elements to an array only if they do not already exist
   - $pop : Removes the first or last item of an array.
   - $pull : Removes all array elements that match a specified query.
   - $pushAll : Deprecated. Adds several items to an array.
   - $push : Adds an item to an array.
   - $pullAll : Removes all matching values from an array.

### **DELETE**
- To remove all documents from a collection pass an empty filter document {} to the db.collection.deleteMany() method
- Delete multiple : db.inventory.deleteMany({})
- Delete single : db.inventory.deleteOne( { status: "D" } )
































