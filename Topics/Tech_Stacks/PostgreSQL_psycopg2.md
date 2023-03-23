# Learning PostgreSQL and psycopg2

## Table of contents
### [Prerequisites](#prerequisites-1)
### [Introduction](#introduction-1)
### [PostgreSQL installation](#PostgreSQL-installation-1)
### [psycopg2 installation](#psycopg2-installation-1)
### [Setup Database and Basic Table Operations in PostgreSQL](#Setup-Database-and-Basic-Table-Operations-in-PostgreSQL-1)
### [Setup and PostgreSQL Operations in psycopg2](#Setup-and-PostgreSQL-Operations-in-psycopg2-1)
### [Additional Resources](#additional-resources-1)

## Prerequisites
Before learning about PostgreSQL and psycopg2, ensure that you have knowledge about the following:
- [Python](https://www.python.org/): High level general purpose programming language.
- Relational Algebra: Understanding the behaviour of relational operations.
- Database Theory: Understanding of constraints, tables, relations, and schemas.
- Basic understanding of SQL: Understand the restrictions of SQL and what information is required to perform operations.

## Introduction
PostgreSQL is an open-source DBMS. As the name states, PostgreSQL is a relational Database Management System (DBMS) based on relations and queries and is great for dealing with large amounts of data and complex queries. It's also good for referencing data quickly and allowing the user to have some flexibility in how they want to represent their data. Furthermore, PostgreSQL supports table inheritance and function overloading.

pyscopg2 is an adapter for Python that allows you to easily integrate PostgreSQL into your program. It's commonly used with other Python libraries like Flask, which allows you to use a PostgreSQL database in your application easily.

## PostgreSQL installation
The following link is to download PostgreSQL onto your computer: https://www.postgresql.org/download/ . This link also shows the different versions of PostgreSQL to match your computer. Follow the instructions after downloading. For your convenience, here are the links to download the installer for PostgreSQL on different OS:
- Windows: https://www.postgresql.org/download/windows/
- MacOS: https://www.postgresql.org/download/macosx/
- Linux: https://www.postgresql.org/download/linux/

Once installed, you can create a database, relation, and tables with the PostgreSQL client called "pgAdmin". pgAdmin is automatically downloaded when using the links above and can be accessed by searching your task bar. You can also perform queries on relations and tables through its query tool. More information on how to use pgAdmin can be found at this [link](https://www.pgadmin.org/docs/pgadmin4/6.21/index.html).

If you are using MacOS, you can also run the command "brew install postgresql" in your terminal. Note that you also have to have Homebrew installed for this command to work. "brew install postgresql" allows the user to use PostgreSQL on their command line by simply initiating a PostgreSQL environment with the command "psql".

For Windows users, the user should download PostgreSQL through the link provided above. If the user wants to utilize PostgreSQL on the command line, they must (after installation):
1. Add the PostgreSQL bin directory path to the PATH environment variable.
2. Run the command "psql -U username"

## psycopg2 installation
To install psycopg2, you can use pip to install its functionality by using the command:
"pip install psycopg2". After installing this in your desired directory, you can import psycopg2 into your python files and perform PostgreSQL queries very intuitively.

## Setup Database and Basic Table Operations in PostgreSQL
A quick and basic runover of PostgreSQL.

### Create Database
To create a database in PostgreSQL, you can either use pgAdmin or the command line. 

In pgAdmin, you can:
1. Open pgAdmin on your computer.
2. Click on "Servers".
3. Click on "PostgreSQL". The version of PostgreSQL should follow after the name.
4. Right click on "Databases" and click "Create"
5. Follow the instructions in pgAdmin.

In the command line:
1. Type "psql" to initialize the PostgreSQL environment.
2. Type "CREATE DATABASE" followed by the name of the database. For example, "CREATE DATABASE CourseInfo".
3. For any errors, you can refer to this [link](https://www.postgresql.org/docs/current/sql-createdatabase.html)


### Create Schema
To create a table, you must first create a schema in your database. 

To do this in pgAdmin:
1. Click on your desired database.
2. Find the "Schemas" directory.
3. Right click and select "Create"
4. Follow the rest of the instructions in pgAdmin

To do this in the command line:
1. Type "psql" to initialize the PostgreSQL environment.
2. Type "\c DBNAME" where DBNAME is the name of the desired database
2. Type "CREATE SCHEMA" followed by the name of the schema. For example, "CREATE SCHEMA SchoolSchema".


### Create Tables
After creating your schema you can create tables/relations to perform operations on. 

To create a table in pgAdmin:
1. Right click on your desired schema.
2. Select "Create"
3. Select "Table"
4. Follow the instructions in pgAdmin

To create a table in the command line:
1. Type "psql" to initialize the PostgreSQL environment.
2. Type "\c DBNAME" where DBNAME is the name of the desired database
3. Type "SET search_path TO schema_name;" where schema_name is the name of the desired schema you want to put your table in.
4. Type "CREATE TABLE table_name (column1 int PRIMARY KEY, ...);", where table_name is the desired name of the table. Inside the round braces is a list of the columns that you want in the table. For each column, you must specify a name and datatype. For example, a table can be created like this:

``` CREATE TABLE accounts (
	id serial PRIMARY KEY,
	username VARCHAR ( 50 ) UNIQUE NOT NULL,
	password VARCHAR ( 50 ) NOT NULL,
	email VARCHAR ( 255 ) UNIQUE NOT NULL,
);
```
The text after the datatypes (e.g. UNIQUE NOT NULL) are optional.

Here is a link for information on datatypes in PostgreSQL: https://www.postgresql.org/docs/current/datatype.html

Here is a link for more details and examples of how to create a table: https://www.postgresql.org/docs/current/sql-createtable.html


### Table Operations
Moving onto table operations. To select data from a certain column in a table, you can use a query like:
``` 
    SELECT col_name1, col_name2 FROM table_name;
```
This gives you a smaller table that only contains the columns "col_name1" and "col_name2" from your selected table in your relation. 

You can also merge two different tables by changing the FROM clause to contain 2 tables:
```
    SELECT col1_table1, col2_table2 FROM table1_name, table2_name;
```
This operation, first, performs a cross product between table1 and table2, where every row of one table is matched with every other row of the other table. Then it selects the data present in the new cross-products table from columns col1_table1 and col2_table2.

In addition, you can perform filtering on tables:
```
SELECT col1_table1, col2_table2 FROM table1_name, table2_name WHERE col1_table1 > 1;
```
Here it only shows data from the previous table where the value of a row in the column "col1_table1" is greater than 1. This is the syntax for when the table and column names between table 1 and table 2 are unique.

There are many other features of PostgreSQL.

Specifics of the syntax of PostgreSQL can be found in this [link](https://www.postgresql.org/docs/current/sql-syntax.html).

## Setup and PostgreSQL Operations in psycopg2
As a quick run over, to start using PostgreSQL in a Python program, you must first set up the psycopg2 module in a Python file. 

This can be done by:

1. Create a database in PostgreSQL. This can be done through the command line or pgAdmin.
Next, all steps are in your python script.
2. "import psycopg2" at the start of your python script.
3. Connect to the new database by running, for example: "conn = psycopg2.connect("dbname=test user=postgres")". In this example, "test" is the name of the database that you created and "postgres" is the default username when you install PostgreSQL.
4. Initialize a cursor with the connection to be able to perform PostgreSQL operations on the database. You can do this by "cur = conn.cursor()"
5. You can execute any PostgreSQL command through this cursor. For example: "cur.execute("SELECT * FROM test;")". This includes commands like creating tables using PostgreSQL syntax.
6. You can use "conn.commit()" to save the changes to your database.
 
Specifics of syntax, such as passing in python variables as values in a query, and module use of psycopg2 can be found in this [link](https://www.psycopg.org/docs/usage.html#passing-parameters-to-sql-queries). The syntax that involves making queries in psycopg2 is the same as PostgreSQL.

There are good examples in the link provided. Here is a link with even more examples to aid you in using psycopg2: https://wiki.postgresql.org/wiki/Psycopg2_Tutorial

## Additional Resources
- This link provides some information on how to link psycopg2 and flask: https://www.geeksforgeeks.org/making-a-flask-app-using-a-postgresql-database/
