## Tech Stacks

### MongoDB

#### 0. Prerequisites:
 - [JavaScript](https://www.w3schools.com/js/): The single most popular and over-powered language in web development used from front-end to back-end.
 - [TypeScript](https://www.typescriptlang.org/): A superset of the Javascript language with type definitions for variables.
 - [Node.js](https://nodejs.org/en/): The most popular runtime environment for JavaScript.
 - [JSON](https://www.json.org/json-en.html): Javascript syntax for objects (instances of classes).
 - [NoSQL](https://www.mongodb.com/nosql-explained): Non-relational databases, which are capable of extremely fast retrieval and simple manipulations of data stored in JSON format, but incapable of complex queries such as joins.

#### 1. Introduction
MongoDB is a popular state-of-the-art NoSQL database compatible with many languages including JavaScript, Python, Java, C#, and so on. It uses JavaScript as its primary query language. It is recommended to use MongoDB with Typescript so that objects will have explicit type constraints as they get passed back and forth between the client and the database. In this short guide, we will introduce [Mongoose](https://mongoosejs.com/docs/), a popular library for creating and manipulating a MongoDB database in the Node.js environment.

#### 2. Set-Up
To create your own MongoDB database for free, create an account on the official [MongoDB website](https://account.mongodb.com/account/login?n=%2Fv2%2F63ebe246adc5d21a1e25f668&nextHash=%23clusters%2Fdetail%2FTestA2) and the rest will be simple and straightforward. You will get a URL for connecting to your own database. Let's name it ```mongoUrl```.

Next, download [Node.js](https://nodejs.org/en/) and install the Mongoose library using the command ```npm install mongoose``` in your project directory.

Now, you can include ```import mongoose from 'mongoose';``` at the top of every code file that uses this library.

A typical project that uses MongoDB has two types of code files that directly use the Mongoose library:
 - Models, which define your database.
 - API handlers, which interact with your database.

#### 3. Defining Your Database
MongoDB stores collections (tables) of documents (rows). Each collection is bascially an entity class and is defined using a "schema".

For example, the ```userSchema``` below specifies that each user document must have a string ```_id```, a string ```name```, and a number ```age```:

```
const userSchema = new mongoose.Schema({
  _id: { type: String, default: () => `user_${nanoid()}`, },
  name: { type: String, required: true },
  age: { type: Number, required: true },
});
```

It is an industry standard to use [nanoid()](https://apoorvtyagi.tech/nanoid-url-friendly-unique-id) to generate unique IDs for a collection. As a result, the ```_id``` field becomes a key for this collection.

It is a commonly used trick to "index" certain fields for constant time search operations based on that field. In this case, if you want to search for a user with a specific name in constant time, simply do ```userSchema.index({ name: 1 }, { unique: false });```.

After creating a schema, you must compile it into a MongoDB model and export it so that other files can access this schema definition:

```
export const User = mongoose.model('User', userSchema);
```

This is all you need to do in the code file that defines your ```User``` model.

#### 4. Interacting with Your Database
To create and store documents as well as to read from or do other manipulations to your database, you must first connect to your database using ```mongoose.connect(mongoUrl);```. Also, don't forget to import your models.

Here is a simple example of how you would create a new document of the ```User``` model and save it to the database:

```
export const createUser = async (name: string, age: number) => {
  const user = new User({
    name: name,
    age: age,
  });
  await user.save();
 }
```

The ```_id``` field is auto-generated, so you do not need to worry about that.

Note that the ```await``` keyword is used for model methods that directly interact with the database to ensure that any code after the method call will not be executed until the method returns. Otherwise, execution order is NOT enforced and you will have to be careful. Any interaction with the database must be done in an ```async``` function. Learn more about them [here](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Statements/async_function).

There are many other [model methods](https://mongoosejs.com/docs/queries.html) that read from or write to the database, such as ```findOne()```, ```updateOne()```, and ```deleteOne()```. 

Congratulations, you now have a solid foundation for knowledge of MongoDB. Use the resources provided to continue your exploration.
