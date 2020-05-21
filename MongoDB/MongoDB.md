# MongoDB Database Notes

### MongoDB is a powerful, flexible, and scalable general-purpose **document-oriented database**. It combines the ability to scale out with features such as secondary indexes, range queries, sorting, aggregations, and geospatial indexes.

- A document-oriented database replaces the concept of a “row” with a more flexible model, the “document” By allowing embedded documents and arrays, the document oriented approach makes it possible to represent complex hierarchical relationships with a  single record

- There are also no predefined schemas: a document’s keys and values are not of fixed types or sizes. Without a fixed schema, adding or removing fields as needed becomes easier

- **Scaling** : MongoDB was designed to scale out. Its document-oriented data model makes it easier for it to split up data across multiple servers.
_MongoDB automatically takes care of_ : 
  1. Balancing data and load across a cluster
  2. Redistributing documents automatically
  3. Routing user requests to the correct machines
  

- When a cluster need more capacity, new machines can be added and MongoDB will figure out how the existing data should be spread to them

