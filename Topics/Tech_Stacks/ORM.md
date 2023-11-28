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
Most applications that you will build, infact most applications that exist today, require some sort of data permimnence. Meaning that data is stored somewhere, and is not lost when a site/app is reloaded. We employ database like MYSQL, PostgreSQL, and MongoDB to ensure that our data can we stored and we can safely interact with it. But how do we do that? There are many database drivers that can allow us to write queries as lines of code directly from within our javascript or python (or whatever language you prefer) scripts.


## What is an ORM:

An ORM (Object Relation Mapper) is a software tool that allows for the translation of an entity between its representaiton in a database (A relation) and object-oriented programming languages (An Object).

As such, they allow us to simply treat all data as objects in our code, and leverage the ORM when we want to store this object in our relational database of choice.

## Example:
Lets take a simple example, where we want to connect to a database, create a user table, and add a new user to our database. How would that look as SQL Queries compared to an ORM? 


<p align="center">
      <img  src="https://github.com/learning-software-engineering/learning-software-engineering.github.io/assets/95612717/b6111831-1240-42f2-868f-76a08647c1db" width="80%" height="50%" display="block">
</p>
<p align="center">
      <img src="https://github.com/learning-software-engineering/learning-software-engineering.github.io/assets/95612717/0faaecfe-2acd-48cc-a5c3-90b89f8833d0" width="80%" height="50%" display="block">
</p>



These screenshots use the following packages for the ORM and raw SQL usage examples, respectively:
1. https://sequelize.org/ 
2. https://node-postgres.com/ 

Looking at the two examples, despite the fact that a similar structure of steps is performed,we can immediatly notice the differences between the 2 stratergies of interacting with databases. The raw SQL stratergy makes heavy use of strings, afterall these strings are directly passed to the database to run the SQL code. On the other hand the ORM method sets up object relation and creates an instance as if it were another object within our code.

## Should I Use One!?

Although the implementation looks different, you can still do everything that ORMS have to offer with just raw SQL queries paired with a database driver and vice versa, so then which one should you actually use? 
As with many choices in the software engineering world (like which langauge to use, or which framework to code in) there is no clear-cut answers. It is your responsibility to understand the . Let us discuss some of these tradeoffs so that you can make a more informed decision, whichever one you choose to use.

### Advantages:

1. **Abstraction of Database Complexity**:  \
Essentially, we allow the people building the code to focus on simply buisness logic, the interactions with the database are also done in object form and they dont need to concern themselves with SQL syntax.

3. **Code Readabilit**y: \
When reading code to see what sections are doing, it is hard to look at SQL strings litered throughout.

5. **Bug-fixing**: \
In our code, we usually get helpful intelissense to avoid silly syntax errors, but what do we do about the syntax errors in our SQL strings? Using an ORM helps us avoid these making our Database code easier to debug.

7. **Different SQL Databases**: \
Different SQL databases have slightly different commands when we get to more complicated logic, when working with an ORM, the ORM deals with this depending on the datbase, but in our raw SQL, we have to change our core logic code when we change our database. 

### Disadvantages:

1. **Performance**: \
The layer of abstraction added by the ORMS also add a another layer of complexity and reduction in performance. Well written SQL code performs much better than an ORM- this ofcourse will scale with the size of a app.

2. **Learning an ORM**: \
It is likely that you the reader probably konws how to write SQL code, but what about Sequelize specifically? Learning an ORM (its syntax, conventions and underlying intricacies) for a projects adds additional prerequisite learning and can delay development 

### Conclusion

So what should you do? ORM or not? It is highly dependant on the needs and constraints of your projecct. An ORM may help you develop rapidly in early stages, and allow the flexibiliy in changes in your database. On the other hand, as your app scales, an ORM may be too slow, and you may want to use raw SQL for optimal performance. Infact, it is not rare to find that big companies have a mix of raw SQL added in later stages alongside legacy ORM code. 

Use whatever you see fit, but be mindful of the consequences coupled with the decisions you make!
