# ORM (Object Relation Mapper)

## Introductions:
Most applications that you will build, in fact most applications that exist today, require some sort of data permanence. Meaning that data is stored somewhere, and is not lost when a site/app is reloaded. We employ databases like MYSQL, PostgreSQL, and MongoDB to ensure that our data can we stored and we can safely interact with it. But how do we do that? There are many database drivers that can allow us to write queries as lines of code directly from within our javascript or python (or whatever language you prefer) scripts. On the other hand, you may consider using an ORM to write your database code!


## What is an ORM:

An ORM (Object Relation Mapper) is a software tool that allows for the translation of an entity between its representation in a database (A relation) and object-oriented programming languages (An Object).

As such, they allow us to simply treat all data as objects in our code, and leverage the ORM when we want to store this object in our relational database of choice.

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
The layer of abstraction added by the ORMS also adds another layer of complexity and reduction in performance. Well-written SQL code performs much better than an ORM- this of course will scale with the size of an app.

2. **Learning an ORM**: \
It is likely that you the reader probably know how to write SQL code, but what about Sequelize specifically? Learning an ORM (its syntax, conventions, and underlying intricacies) for projects adds additional prerequisite learning and can delay development 

### Conclusion

So what should you do? ORM or not? It is highly dependent on the needs and constraints of your project. An ORM may help you develop rapidly in early stages, and allow flexibility in changing your database. On the other hand, as your app scales, an ORM may be too slow, and you may want to use raw SQL for optimal performance. In fact, it is not rare to find that big companies have a mix of raw SQL added in later stages alongside legacy ORM code. 

Use whatever you see fit, but be mindful of the consequences coupled with the decisions you make!
