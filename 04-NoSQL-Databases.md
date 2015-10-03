# NoSQL Databases

## Databases Systems
* A database is a storage where information can be stored
  * Information meaning computer information like numbers and strings
* Two common types of database systems
  * Relational databases and Non-relational databases
* Relational databases
  * Data stored as table rows
  * Relationships between related rows
  * Single entity spans multiple tables
  * RDBMS systems are very mature, rock solid
* NoSQL databases
  * Data stored as documents
  * Single entity (document) is a single record
  * Documents do not have a fixed structure

## NoSQL Databases
* NoSQL databases save data in non-relational way
  * The data is stored in many documents
  * Records in a document can be different
  * Documents can have nested documents
* NoSQL databases provide simplicity of design and availability
* Used mostly when in need to keep big data or in real-time web apps
* Non-Relational Data Models
  * Document model
    * Set of documents, e.g. JSON strings
  * Key-value model
    * Set of key-value pairs
  * Hierarchical key-value
    * Hierarchy of key-value pairs
  * Wide-column model
    * Key-value model with schema
  * Object model
    * Set of OOP-style objects

## NoSQL Database Systems
* Redis
  * Ultra-fast in-memory data structures server
* MongoDB
  * Mature and powerful JSON-document database
* CouchDB
  * JSON-based document database with REST API
* Cassandra
  * Distributed wide-column database
  
![NoSQL Database Systems](https://github.com/huytrongnguyen/aspnet5/blob/master/css/imgs/nosql-database-systems.png)

## MongoDB
* MongoDB is an open-source document store database
  * Save JSON-style objects with dynamic schemas
  * Support for indices
  * Has document-based queries
    * CRUD operations
* A MongoDB instance can have many databases
  * A database can have many collections
    * A collection can have many documents

## What is Redis?
* Redis is
  * Ultra-fast in-memory key-value data store
  * Powerful data structures server
  * Open-source software: http://redis.io
* Redis stores data structures:
  * Strings
  * Lists
  * Hash tables
  * Sets / sorted sets

## The JSON Data Format
* JSON (JavaScript Object Notation) is a lightweight data format
  * Human and machine-readable
  * Based on the way to create objects in JS
  * Platform independent – can be used with any programming language
