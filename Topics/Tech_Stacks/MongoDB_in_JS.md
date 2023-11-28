# Using MongoDB with JavaScript

## Table of contents
### [Introduction](#introduction-1)
### [Installation](#installation-1)
### [Setting up a MongoDb database](#setting-up-a-mongodb-database-1)
### [Connecting to a MongoDB database](#connecting-to-a-mongodb-database-1)
### [Accessing/Modifying your database](#accessingmodifying-your-database-1)
### [Creating a document](#creating-a-document-1)
### [Reading a document](#reading-a-document-1)
### [Updating a document](#updating-a-document-1)
### [Deleting a document](#deleting-a-document-1)
### [Additional Resources](#additional-resources-1)

## Introduction

This is an introduction to MongoDB basics in JavaScript. This article assumes that the reader has a decent understanding of JavaScript.

MongoDB is a cross-platform document-oriented database program that uses JSON-like documents to store data.

In this article we will cover the basics of connecting to and modifying the contents of MongoDB databases using JavaScript.

## Installation

MongoDB can be installed using npm by running `npm install mongodb` in the termimal.

MongoDB has a free, open-source GUI available called MongoDB Compass, which is highly reccomended for visualizing the data in your DB. It can be downloaded [here](https://www.mongodb.com/try/download/compass).

## Setting up a MongoDB database

You can set up a MongoDB deployment MongoDB Atlas, which you can sign up for for free [here](https://www.mongodb.com/atlas). Once registered, there will be a newly created project with a deployment created. More can be created as needed through the website, or through MongoDB Compass.

## Connecting to a MongoDB database

To connect to your new deployment,

To connect via MongoDB Compass, click on 'MongoDB Compass' and copy the connection string into the 'New Connection' box in Compass. Be sure to replace the password segment of the string as instructed on the connect page.

To connect via your Node.js application, first in the JS file we must create a MongoClient object, which will allow us to create connections to MongoDB databases. The only necessary attribute is `url`, which should be the provided connection string which can be found on MongoDB Atlas.

To get your connection string, go to the database tab in MongoDB Atlas and click the 'Connect' button. A menu will pop up giving you several different options for connecting. Click on 'drivers', and there will be the connection string.

For example, to initialize a MongoClient object for the demo DB, I would use the following code: 

```
// My MongoDB's connection string
const conn_string = "mongodb+srv://esicheri:Spaghetti12@wackycluster0.etikgsf.mongodb.net/?retryWrites=true&w=majority";
const client = new MongoClient(conn_string);
```

Once you have created your MongoClient object, use the .connect() method to create a connection to the MongoDB deployment, and get a db instance of a database of our choice by using the .db() method and giving it the name of the database we want as a parameter.

For example, after executing the code above, to access a database called "sample_guides", I would use the following code:

```
await client.connect();
db = client.db("sample_guides");
```

Altogether, and with a bit of error handling sprinkled in, we get this code, which I've put in a file called `database.js`:

```
const { MongoClient } = require('mongodb');
const conn_string = "mongodb+srv://esicheri:Spaghetti12@wackycluster0.etikgsf.mongodb.net/?retryWrites=true&w=majority";
const database = "sample_guides";

const client = new MongoClient(conn_string);

async function connectDatabase() {
  try {
    await client.connect();
    return client.db(database);
  } catch (err) {
    console.error(err);
    throw err;
  }
}

module.exports = {
  connectDatabase,
};
```

I will be using this function later when modifying the database contents.


## Accessing/Modifying your database

For this section, we'll be givng examples using the sample dataset provided by MongoDB. If you want to follow along, select your database in MongoDB Atlas, go to the 'Collections' tab, and if it's empty there should be an option to 'Load Sample Dataset'. This will load the sample data that we will be using for the examples. In paricular, we will be using the sample_guides database, which contains information on planets.

For this tutorial, we'll be showing you how to perform the 4 CRUD operations: Create, Read, Update and Delete.

### Creating a Document

To create a single document, we can use the .insertOne() method. This method takes as a parameter an object mapping field names to their desired contents. 

For example, if I wanted to add some information to the 'planets' collection in the sample_guides database, I could use the following function:

```
async function createDoc(name, orderFromSun, hasRings, mainAtmosphere, surfaceTemperatureC) {
  // Calls our function from earlier to get a db instance
  const database = await connectDatabase();
  // gets the planets collection
  const collection = database.collection("planets");

  const insert = await collection.insertOne({
    name: name, 
    orderFromSun: orderFromSun, 
    hasRings: hasRings, 
    mainAtmosphere: mainAtmosphere,
    surfaceTemperatureC: surfaceTemperatureC
  });
  return insert;
}
```
This function takes takes values for each field and then creates a new document with those values in their associated fields.

Say that we decide that Pluto is a planet after all, and wanted to add some information about it to our collection of planets. Then we could call the function with the desired values:

`createDoc("pluto", 9, false, ["N2", "CH4", "CO"], {min: -233, max: -223, mean: -225});`

and a new document with those values would be added to planets.

.insertOne returns a document with a boolean value 'acknowledged' and a field 'insertedId' which contains the ObjectID of the newly created document. For example, when I ran the above code, it returned 
```
{
  acknowledged: true,
  insertedId: new ObjectId('6563e3576df681ce14e61470')
}
```

### Reading a Document

To retrieve a document, we can use the .findOne() method. .findOne() takes 3 parameters:  

To learn more about query operators for djangoDB, you can find documentation [here](https://www.mongodb.com/docs/rapid/reference/operator/query/#std-label-query-projection-operators-top). For now however we'll stick with something sinmple and search up a document by its object id.

For example, the following function takes a string of an ObjectId of the document we want to retrieve, then returns that document:

```
async function getDoc(id) {
  const database = await connectDatabase();
  const result_collection = database.collection("planets");

  return await result_collection.findOne({
    _id: new ObjectId(id),
  });
}
```
Notice how we don't pass the string into the query directly. This is because in MongoDB id fields hold a special ObjectId object, instead of just a string. So in order to find the document based of the string passed in, we must create a new ObjectId object to pass to the query.

Now, to access the document we created in the last example, we can run `getDoc('6563e3576df681ce14e61470')`, which returns the following:

```
{
  _id: new ObjectId('6563e3576df681ce14e61470'),
  name: 'pluto',
  orderFromSun: 9,
  hasRings: false,
  mainAtmosphere: [ 'N2', 'CH4', 'CO' ],
  surfaceTemperatureC: { min: -233, max: -223, mean: -225 }
}
```

### Updating a Document

To update a document, we can use the .updateOne method. This method takes as parameters a query object like .findOne() does, and an update document that contains of update operators. The method finds the desired document in the collection based off of the query object, then applies the supplied update operators to the found document.

There are many different update operators, which you can learn about [here](https://www.mongodb.com/docs/manual/reference/operator/update/#std-label-update-operators). In this tutorial, we'll use a simple one: $set. $set allows you to update the values of fields in a document by supplying a document containing the desired replacement values.

For eaxmple, the function below takes an id value and a name string, then finds the document with the given id and updates its name field:
```
async function updateName(id, name) {
  const database = await connectDatabase();
  const collection = database.collection("planets");

  const update = await collection.updateOne(
    // The query:
    { _id: new ObjectId(id) },
    // The fields:
    { $set: { name: name}
    }
  );
  return update;
}
```
Oops! It seems I forgot to put a capital P at the beginning of the word Pluto earlier. To update our Pluto document to correct our spelling mistake, we can call `updateDoc('6563e3576df681ce14e61470', "Pluto");`. If we then run `getDoc('6563e3576df681ce14e61470')` again, it returns:
```
{
  _id: new ObjectId('6563e3576df681ce14e61470'),
  name: 'Pluto',
  orderFromSun: 9,
  hasRings: false,
  mainAtmosphere: [ 'N2', 'CH4', 'CO' ],
  surfaceTemperatureC: { min: -233, max: -223, mean: -225 }
}
```

There! Much better.

### Deleting a Document

To delete a document, we can use the .deleteOne() method. Like findOne, deleteOne accepts a query as a parameter that tells it which document to delete. Again, for simplicity, we'll have it search by id.

The following function takes a string of a document's ObjectId and finda and deletes that document:
```
async function deleteDoc(id) {
  const database = await connectDatabase();
  const collection = database.collection("planets");

  const del = await collection.deleteOne(
    // The query
    { _id: new ObjectId(id) }
  );
  return del.deletedCount;
}
```

Say that after all that work, we decide that Pluto isn't a planet after all, and we want to delete the Pluto document from our collection. We can run `deleteDoc('6563e3576df681ce14e61470')`, and the next time we run  `getDoc('6563e3576df681ce14e61470')`, it returns `null`. All gone!

## Additional Resources

MongoDB is a powerful tool for database management. We only went over the basics in this tutorial, and there's so much more to learn.

The full documentation for MongoDB can be found [here](https://www.mongodb.com/docs/).
