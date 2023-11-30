# ORM (Object Relation Mapper)

## Table of Content
### [Introductions](#introductions-1)
### [What is an ORM](#what-is-an-orm-1)
### [Example](#example-1)
### [Should I use one?](#should-i-use-one-1)
### [Advantages](#advantages-1)
### [Disadvantages](#disadvantages-1)
### [Conclusion](#conclusion-1)

## Introductions:
Most applications that you will build, in fact most applications that exist today, require some sort of data permanence. Meaning that data is stored somewhere, and is not lost when a site/app is reloaded. We employ databases like MYSQL, PostgreSQL, and MongoDB to ensure that our data can be stored and we can safely interact with it. But how do we do that? There are many database drivers that can allow us to write queries as lines of code directly from within our javascript or python (or whatever language you prefer) scripts. On the other hand, you may consider using an ORM to write your database code!


## What is an ORM:

An ORM (Object Relation Mapper) is a software tool that allows for the translation of an entity between its representation in a database (A relation) and object-oriented programming languages (An Object). As such, they allow us to simply treat all data as objects in our code, and leverage the ORM when we want to store this object in our relational database of choice. 

- Its good to node that ORM alternatives exist for non-relational databases too, these would be ODMs (Object Document Models), for example, MongoDB has one called mongoose which applies to javascript/typescript. A lot of these discussions apply to these ODMs too. 

## Example:
Let's take a simple example, where we want to connect to a database, create a user table, and add a new user to our database. How would that look as SQL Queries compared to an ORM? 

```js
// First the example using an ORM!
import {Sequelize, DataTypes} from 'sequelize'

const sequelize = new Sequelize(); //Server details go here

const Student = sequelize.define('Student', {
    id: {
        type: DataTypes.INTEGER,
        primaryKey: true,
        autoIncrement: true
    },
    username: {
        type: DataTypes.STRING,
        allowNull: false,
    },
    student_number: {
        type: DataTypes.INTEGER,
        allowNull: false,
    },
})


// Note: await simply forces the code to wait for the asynchronous code to resolve before proceeding, such as syncing to the database. 
await Student.sync({force:true}); // Ensures table is created in DB

await Student.create({
    username: 'sidiki',
    student_number: 6789998212
})

await sequelize.close()
```

```js
// The following is the equivalent code using RAW SQL more heavily
import { Client } from 'pg'
const client = new Client() // Server Details go here
await client.connect()

const createTableQuery = await client.query(
    ```
    Create TABLE Student (
        id SERIAL PRIMARY KEY,
        username varchar(50),
        student_number integer
    );
    ```
)

const student_username = "sidiki" 
const student_number = 6789998212 

const insertQuery = await client.query(
    ```
    Insert into Student (username, student_number) Values 
    ('${student_username}', ${student_number});
    ```
)

await client.end()

```

These screenshots use the following packages for the ORM and raw SQL usage examples, respectively:
1. https://sequelize.org/ 
2. https://node-postgres.com/ 

Looking at the two examples, despite the fact that a similar structure of steps is performed, we can immediately notice the differences between the 2 strategies of interacting with databases. The raw SQL strategy makes heavy use of strings, after all these strings are directly passed to the database to run the SQL code. On the other hand, the ORM method sets up object relation and creates an instance as if it were another object within our code.


## Should I Use One!?

Although the implementation looks different, you can still do everything that ORMS have to offer with just raw SQL queries paired with a database driver and vice versa, so then which one should you actually use? 
As with many choices in the software engineering world (like which language to use, or which framework to code in) there are no clear-cut answers. It is your responsibility to understand the advantages and disadvantages of the two options and make an informed decision on how you will be interacting with your database. Let us discuss some of these tradeoffs so that you can make a more informed decision, whichever one you choose to use.

### Advantages:

1. **Abstraction of Database Complexity**:  \
Essentially, we allow the people building the code to focus simply on the business logic; the interactions with the database are also done in object form and they do not need to concern themselves with SQL syntax.

3. **Code Readabilit**y: \
When reading code to see what sections are doing, looking at SQL strings littered throughout is hard. On the other hand, the readability of ORM code (the database interactions being mainly through methods and attributes of the Data Model objects) makes it much easier to follow.

5. **Bug-fixing**: \
In our code, we usually get helpful IntelliSense to avoid silly syntax errors, but what do we do about the syntax errors in our SQL strings? Using an ORM helps us avoid these making our Database code easier to write and debug.

7. **Different SQL Databases**: \
Different SQL databases have slightly different commands when we get to more complicated logic, when working with an ORM, the ORM deals with this depending on the database, but in our raw SQL, we have to change our core logic code when we change our database. 

### Disadvantages:

1. **Performance**: \
The layer of abstraction added by the ORMS also adds another layer of complexity and reduction in performance. Well-written SQL code performs much better than an ORM- this of course will scale with the size of an app (by performance we mean how quickly queries execute and return).

2. **Learning an ORM**: \
It is likely that you the reader probably know how to write SQL code, but what about Sequelize specifically? Learning an ORM (its syntax, conventions, and underlying intricacies) for projects adds additional prerequisite learning and can delay development 

### Conclusion

So what should you do? ORM or not? It is highly dependent on the needs and constraints of your project. An ORM may help you develop rapidly in early stages, and allow flexibility in changing your database. On the other hand, as your app scales, an ORM may be too slow, and you may want to use raw SQL for optimal performance. In fact, it is not rare to find that big companies have a mix of raw SQL added in later stages alongside legacy ORM code. 

Use whatever you see fit, but be mindful of the consequences coupled with the decisions you make!
