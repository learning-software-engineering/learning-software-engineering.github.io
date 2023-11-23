# Introduction to interactions between NoSQL database and JSON
## NoSQL database overview
NoSQL databases represent a broad category of database management systems that differ from traditional relational databases in their data model, query languages, and consistency models. The term "NoSQL" stands for "Not Only SQL" or “non-relational”, reflecting the fact that these databases may not use relational tables with predefined schemas to store data. NoSQL databases use flexible data models that can adapt to changes in data structures and are capable of scaling easily with large amounts of data and high user loads. 

_Note: We assume you have the basic knowledge about JSON, please refer to this [link](https://www.w3schools.com/js/js_json_intro.asp) if you want to learn more about JSON._

## Types of NoSQL databases
Behind the big category of NoSQL databases, there are four major types of databases that are broadly used nowadays.
+ **Key-value databases**
The simplest form of NoSQL databases, they store data as a collection of key-value pairs. The key is a unique identifier, and each of them corresponds to a value, which is the data associated with it.

+ **Wide-Column Stores**
These databases store data in tables, rows, and dynamic columns. Unlike relational databases, the schema can vary from row to row in the same table.

+ **Graph Databases**
Graph databases use graph structures with nodes, edges, and properties to represent and store data. The relationships are first-class entities in these databases.

+ **Document databases**
These databases store data in documents, which are typically JSON-like structures. Each document contains pairs of fields and values. The values can typically be a variety of types including things like strings, numbers, booleans, arrays, or objects.

We will focus on the Document-Oriented Databases here as the documents are very similar to JSON objects. Further, we will discuss the interaction between document databases and JSON including importing, storing, querying and indexing JSON data with the advantages of JSON document databases.

## Document Database - JSON interaction

In this guide, we'll use MongoDB as an example, but the process is similar for other document databases.

### Importing JSON Data
After installing the MongoDB Community Edition and MongoDB Compass, you can use the mongoimport command-line tool, which is part of the MongoDB server installation.

Navigate to the directory containing your JSON file, then open your command line or terminal, run the `mongoimport` command with the necessary parameters. For example:

```
mongoimport --db mydatabase --collection mycollection --file mydata.json --jsonArray
```

+ `--db mydatabase`: Specifies the database name.
+ `--collection mycollection`: Specifies the collection.
+ `--file mydata.json`: Specifies the path to your JSON file.
+ `--jsonArray`: Indicates that the JSON file contains an array of documents.

To verify if JSON files have been imported correctly, use MongoDB Compass or the MongoDB shell to connect to your database and check if the data has been imported correctly. 

Moreover, you can always use programming languages like Java and Python to import JSON files, or using MongoDB Compass directly, see [here](https://www.mongodb.com/compatibility/json-to-mongodb)for instructions.

### Storing JSON Data
Storing JSON data in MongoDB is a seamless process due to its native support for JSON-like structures. There are mainly two ways to store JSON data in a Document-Oriented database:

Store the whole object in a single document.
Example:

```
book {
   title: 'Moby Dick',
   author: {
       name: 'Herman Melville',
       born: 1819
   }
}
```

Here, the author details are inside the book document itself. This technique is also known as embedding because the author subdocument is embedded in the book document.

Store parts of objects separately and link them using the unique identifiers (referencing).
Example:
```
author {
  _id: ObjectId(1),
  name: 'Herman Melville',
  born: 1819
}

book {
  _id: ObjectId(55),
  title: 'Moby Dick',
  author: ObjectId(1)
}
```
One author may write multiple books. So, to avoid duplicating data inside all the books, we can create separate author documents and refer to it by its `_id` field.

After making sure how you want to store your data, use `insertOne`  or `insertMany` methods to insert your document to desired collections:

```
db.mycollection.insertOne({/* JSON-structure object */});
```
or
```
db.mycollection.insertMany([/* array of JSON documents */]);
```

### Querying JSON Data
MongoDB queries are expressed as JSON-like structures, allowing you to easily query fields within documents using the build-in find method with following parameters.
```
db.collection.find( <query>, <projection>, <options> );
```
`<query>`: specify the search criteria for the query. It's essentially a filter that selects which documents to include based on their fields' values.
If you want to look for something with some specific values, just put `{ “field1”: <value1>, “field2”: <value2>, ...}`
For example, to find documents where name is "John", you can simply use:
```
db.collection.find({ "name": "John" })
```

You can also use comparison operators like `$gt` (greater than), `$lt` (less than), `$eq` (equal), etc. and logical operators like `$and,` `$or`, and `$not` to build complex queries.
For example, to find documents where the age field is greater than 25, use `$gt`.
```
db.collection.find({ "age": { "$gt": 25 } });
```
To find documents where age is greater than 25 and name is "John":
```
db.collection.find({ "$and": [{ "age": { "$gt": 25 } }, { "name": "John" }] })
```
You can query nested fields by using dot notation 
```
“<embedded document>.<field>”
```
For example, to find documents where the city in the address is "Anytown":
```
db.collection.find({ "address.city": "Anytown" })
```

To query for array elements
For example, If a document has a field tags that is an array, to find documents containing a tag "mongodb":
```
db.collection.find({ "tags": "mongodb" })
```


`<projection>`: Specifies the fields to return in the documents that match the query filter. The parameter contains either include or exclude specifications, not both, unless the exclude is for the `_id` field.

For example, to return only the name and age fields of documents
```
db.collection.find({}, { "name": 1, "age": 1, "_id": 0 })
```
Here, 1 indicates inclusion of the field.

`<options>`: Specifies additional options for the query. These options modify query behavior and how results are returned. 
This parameter is not passed directly into the `find()` method like the `<query>` and `<projection>` parameters. Instead, `<options>` are specified through method chaining, where you append methods to `find()` that correspond to the various options you want to apply, such as sorting, limiting, and skipping documents.

For example, you can use `sort()` to sort the results based on one or more fields.
```
db.collection.find().sort({ "age": 1 })
```
Here, we sort documents by age in ascending order.

To restrict the number of documents returned, use limit().
```
db.collection.find().limit(5)
```
We limit the query to return only 5 documents here.

To get a more specific result, you can combine the option method together, for example combine `limit()` and `skip()` for pagination.
```
db.collection.find().skip(5).limit(5)
```
We will get the second set of 5 documents in this case. 

There are many more available options, visit here for more details.

Note every parameter above is optional, to return all documents in a collection, omit all parameters or pass an empty document ({}).

### Indexing JSON Data
Indexing JSON data in a NoSQL database like MongoDB is crucial for optimizing query performance. An index in a MongoDB database is a special data structure that stores a small portion of the collection's data in an easy-to-traverse form. The index stores the value of a specific field or set of fields, ordered by the value of the field as specified in the index.

The purpose of indexing is that it supports the efficient execution of queries. Without indexes, MongoDB must perform a collection scan, i.e., scan every document in a collection, to select those documents that match the query statement.

There are many type of indexes in NoSQL databases:
+ Single Field: Apart from the _id field, which is automatically indexed, you can create indexes on any field in a document.
+ Compound Index: Indexes multiple fields in a single index.
+ Multikey Index: Automatically created for fields that hold arrays; used to index array elements.
+ Text Index: Created to enable text search on string content.
+ Hashed Index: Indexes the hash of the value of a field.
Indexes have the property to be unique, which ensures that two documents cannot have the same value for the indexed field. They can be created with a specified order (ascending or descending).
We will give some examples for some common types of indexes using createIndex method:

Single Field Index: To create an index on a single field
```
db.collection.createIndex({ "fieldname": 1 }) // 1 for ascending order
```
Compound Index: To index multiple fields, specify each field and its sort order
```
db.collection.createIndex({ "field1": 1, "field2": -1 }) // 1 for ascending, -1 for descending
```
Text Index: To enable text search
```
db.collection.createIndex({ "fieldname": "text" })
```

## Advantages of JSON Structure Database
### Better schema flexibility
The best part of a JSON document database is the schema flexibility, unlike relational databases, JSON databases allow for a flexible and dynamic schema, meaning the structure of data can be changed without impacting existing data.They easily store and manage complex data types, including nested documents and arrays.

### Faster and have more storage flexibility
NoSQL databases, in general, have more storage flexibility and offer better indexing methods. In a document database, each document is handled as an individual object, and there is no fixed schema, so you can store each document in the way it can be most easily retrieved and viewed. Additionally, you can evolve your data model to adapt it to your changing application requirements. 

### Better suited for big data analytics
JSON structure databases have a flexible schema and are often designed to scale out horizontally, distributing data across multiple servers, which is beneficial for handling large volumes of data. Further, these databases can easily pass data to popular data analysis programming languages like Python and R, without additional coding steps.

## Reference 
https://www.mongodb.com/nosql-explained
https://www.w3schools.com/js/js_json_intro.asp
https://www.mongodb.com/docs/manual/core/document/
https://www.mongodb.com/json-and-bson
https://www.mongodb.com/docs/manual/core/databases-and-collections/
https://www.mongodb.com/docs/manual/reference/method/db.collection.find/
https://mongodb.github.io/node-mongodb-native/4.0//interfaces/findoptions.html
https://www.mongodb.com/docs/manual/reference/method/db.collection.find/#std-label-method-find-projection
OpenAI. (2023, Nov 22). ChatGPT: A Language Model by OpenAI. Retrieved Nov 22, 2023 from https://www.openai.com/research/chatgpt


