# Understanding SQL Schemas, Database Creation, and Best Practices for Optimal Setup

## Table of Contents
1. [Introduction to SQL](#introduction-to-sql)
2. [Understanding Schema in SQL](#understanding-schema-in-sql)
3. [Steps for Basic Database Creation](#steps-for-basic-database-creation)
    1. [How to create a schema](#how-to-create-a-schema)
    2. [How to create tables in the schema](#how-to-create-tables-in-the-schema)
    3. [Datatypes](#datatypes)
    4. [Reaction policies](#reaction-policies)
4. [Best Practices for Database Structure](#best-practices-for-database-structure)

### Introduction to SQL
SQL also known as Structured Query Language is a programming language used to store and process information in a relational database.
When working with databases in your projects, it is a very helpful language to easily manage and manipulate data.
It also integrates well with different programming languages making it a very efficient tool.

To learn more about what SQL is, check out [What is SQL (Structured Query Language)?](https://aws.amazon.com/what-is/sql/#:~:text=Structured%20query%20language%20(SQL)%20is,relationships%20between%20the%20data%20values).

### Understanding Schema in SQL
In a SQL database, a schema is a list of logical structures of data. It's a way to organize and manage database objects. A schema helps to segregate and structure the database by providing a namespace for these objects.

It allows different users or applications to have their own space within the database without conflicting with each other's objects.

To read more about schema and their advantages, you can check out
[What Is a Schema in SQL and Advantages of Using Schema](https://www.simplilearn.com/tutorials/sql-tutorial/schema-in-sql#:~:text=MEANExplore%20Program-,What%20is%20Schema%20in%20SQL%3F,user%20who%20constructs%20the%20object).

### Steps for Basic Database Creation

#### How to create a schema
The first step of a good database creation should be to initialize a schema.
<br>
You can do so by
<br>CREATE SCHEMA <schema name>; <br>
and then alter the schema to add tables to it.

You can alternatively use,<br>
CREATE SCHEMA <schema name> <br>
CREATE TABLE table_name (...);

#### How to create tables in the schema
A table is a fundamental structure used to store data in a relational database. It consists of rows and columns where each column represents a different attribute, and each row represents a record or an entry in the table

The syntax to create a table is
CREATE TABLE <tablename> (<column1_name column1_datatype other_attributes,
column2_name column2_datatype other_attributes,...);

Example :
CREATE SCHEMA University
CREATE TABLE Students(
    utorid varchar(8),
    fname varchar(15),
    lname varchar(15)
);

![example_table_creation](https://github.com/learning-software-engineering/learning-software-engineering.github.io/assets/113269746/233e090d-a9ef-4fdc-9fbd-db8fc1870558)



Links :<br>
https://www.w3schools.com/sql/sql_create_table.asp
https://www.w3schools.com/sql/sql_alter.asp

#### Datatypes
SQL has a range of datatypes your column can have.

Check https://www.w3schools.com/sql/sql_datatypes.asp for the list of datatypes, their description and storage.

#### Reaction policies
Reaction policies are actions defined on a database level to manage referential integrity constraints, especially when a referenced record is affected by a change (update or delete).
Some of the most common reaction policies are :
- CASCADE<br>
  This action propagates the changes (update or delete) to the related rows automatically. For instance, if a record in a parent table is deleted, CASCADE will automatically delete all related records in the child table that reference the deleted record.
- SET NULL<br>
  With this action, if a referenced record is deleted or updated, the foreign key columns in the referencing table are set to NULL. This means the reference will no longer exist.
- RESTRICT<br>
  This action prevents changes that would violate referential integrity. For instance, it prevents the deletion or update of a referenced record if there are still related records in the referencing table.

### Best Practices for Database Structure
When it comes to practices, there are a lot of practices that one can adopt in order to build a nice and efficient. Here are some of the main things to keep in mind while building a database.

1. Avoid redundancy

Redundancy refers to the unnecessary repetition or duplication of data within a database. Redundancy can occur when the same data is stored in multiple places or when unnecessary columns are present in a table.
<br>
There are many ways to reduce redundancy and one of the ways is to normalize your data. There are algorithms like BCNF Decomposition, 3CNF etc. which can be useful.

Links to check out:
- https://www.mydbsync.com/blogs/ways-to-reduce-data-redundancy/
- https://www.linkedin.com/advice/1/how-do-you-normalize-your-data-reduce-redundancy

2. Use primary and foreign keys

A primary key is a key used to uniquely identify a row in a table and cannot have NULL values.
<br>
A foreign key is a key that refers to a column in a relational database table that provides a link between data in two tables. It is a column (or columns) that references a column (most often the primary key) of another table.
<br>
Utilize these keys effectively to establish relationships between tables, enforcing data integrity and ensuring referential integrity.

3. Use consistent naming conventions


4. Avoid designing your schema in such a way that there are attributes that can be null.

These are just some ideas and tips to create a basic schema. SQL is a very powerful languages, and you can do a lot more using it!
