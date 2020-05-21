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



























