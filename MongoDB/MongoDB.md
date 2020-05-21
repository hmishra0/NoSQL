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







