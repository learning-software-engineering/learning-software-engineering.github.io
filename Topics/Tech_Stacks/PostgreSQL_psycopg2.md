# Learning PostgreSQL and psycopg2

## Table of contents
### [Prerequisites](#prerequisites-1)
### [Introduction](#introduction-1)
### [PostgreSQL Installation](#postgresql-installation-1)
### [psycopg2 Installation](#psycopg2-installation-1)
### [Setup Database and Basic Table Operations in PostgreSQL](#setup-database-and-basic-table-operations-in-postgresql-1)
### [Setup and PostgreSQL Operations in psycopg2](#setup-and-postgresql-operations-in-psycopg2-1)
### [Additional Resources](#additional-resources-1)

## Prerequisites
Before learning about PostgreSQL and psycopg2, ensure that you have knowledge about the following:
- [Python](https://www.python.org/): High level general purpose programming language.
- Relational Algebra: Understanding the behaviour of relational operations.
- Database Theory: Understanding of constraints, tables, relations, and schemas.
- Basic understanding of SQL: Understand the restrictions of SQL and what information is required to perform operations.

## Introduction
PostgreSQL is an open-source DBMS. As the name states, PostgreSQL is a relational Database Management System (DBMS) based on relations and queries and is great for dealing with large amounts of data and complex queries. It's also good for referencing data quickly and allowing the user to have some flexibility in how they want to represent their data. Furthermore, PostgreSQL supports table inheritance and function overloading.

pyscopg2 is an adapter for Python that allows you to easily perform PostgreSQL operations in your Python programs. It's commonly used with other Python libraries like Flask, which collectively allow you to modify a PostgreSQL database in your application with minimal hassle.

## PostgreSQL installation
The following link is to download PostgreSQL onto your computer: [https://www.postgresql.org/download/](https://www.postgresql.org/download/) . This link also shows the different versions of PostgreSQL to match your computer. Follow the instructions after downloading and make sure to remember the username and password during setup. For your convenience, here are the links to download the installer for PostgreSQL on different OS:
- Windows: [https://www.postgresql.org/download/windows/](https://www.postgresql.org/download/windows/)
- MacOS: [https://www.postgresql.org/download/macosx/](https://www.postgresql.org/download/macosx/)
- Linux: [https://www.postgresql.org/download/linux/](https://www.postgresql.org/download/linux/)

If you are using MacOS, you can also run the command `brew install postgresql` in your terminal. Note that you also have to have Homebrew installed for this command to work. `brew install postgresql` allows the user to use PostgreSQL on their command line by simply initiating a PostgreSQL environment with the command `psql`. More information can be found [here](https://www.moncefbelyamani.com/how-to-install-postgresql-on-a-mac-with-homebrew-and-lunchy/).

For Windows users, the user should download PostgreSQL through the link provided above. If the user wants to utilize PostgreSQL on the command line, they must (after installation):
1. Add the PostgreSQL bin directory path to the PATH environment variable.
2. Run the command `psql -U <username>`, where `<username>` is the username you selected during installation.

Once installed, you can create a database, relation, and tables with the PostgreSQL client called **pgAdmin**. **pgAdmin** is automatically downloaded when using the links above and can be accessed by searching your task bar. (If you are using Homebrew, you have to install **pgAdmin** separately by running `brew install --cask pgadmin4`.) You can also perform queries on relations and tables through its query tool. More information on how to use **pgAdmin** can be found at this [link](https://www.pgadmin.org/docs/pgadmin4/6.21/index.html).

## psycopg2 Installation
To work with psycopg2, you can use pip to install it by running `pip install psycopg2` in your console. Make sure you execute this command in the directory you will be using psycopg2. Once finished, you can import psycopg2 (`import psycopg2` at the top of the relevant Python file), and perform the desired operations.

## Setup Database and Basic Table Operations in PostgreSQL
A quick and basic runover of PostgreSQL.

### Create Database
To create a database in PostgreSQL, you can either use pgAdmin or the command line. 

In pgAdmin, you can:
1. Click on **Servers**.
2. Click on **PostgreSQL**. The version of PostgreSQL should follow after the name.
3. Right click on **Databases** and click **Create**
4. Follow the instructions in pgAdmin.

In the command line:
1. Type `psql` to initialize the PostgreSQL environment.
2. Type `CREATE DATABASE dbname;`, where `dbname` is the name of the database to create.
Documentation on setting database parameters can be found [here](https://www.postgresql.org/docs/current/sql-createdatabase.html).


### Create Schema
To create a table, you must first create a schema in your database. 

To do this in pgAdmin:
1. Click on your desired database.
2. Right click the **Schemas** directory and select **Create**.
3. Fill in the fields on the dialog and press **Save**.

To do this in the command line:
1. Execute `psql` to initialize the PostgreSQL environment.
2. Execute `\c dbname;` where `dbname` is the name of the desired database.
3. Run `CREATE SCHEMA schema_name;`. If the operation was successful, you should see the message `CREATE SCHEMA` on the next line.
4. Run `\dn` to get a list of available schemas.


### Create Tables
After creating your schema you can create tables/relations to perform operations on. A table contains columns, which describes the attributes of the data being stored, and rows, which are record of intances of the table. Each row contains a set of values that corresponds to the columns of the table.

To create a table in pgAdmin:
1. Right click on your desired schema.
2. Select **Create** then **Table**.
4. Follow the instructions in pgAdmin.

To create a table in the command line:
1. Execute `psql` to initialize the PostgreSQL environment.
2. Execute `\c dbname` where `dbname` is the name of the desired database
3. Run `SET search_path TO schema_name;` where `schema_name` is the name of the schema you want to put your table in.
4. Type `CREATE TABLE table_name (column1 int PRIMARY KEY, ...);`, where `table_name` is the name of the table to create. Inside the round braces is a list of the columns that you want in the table. For each column, you must specify a name and datatype. For example, a table can be created like this:

```
CREATE TABLE sports (
	sport_id SERIAL PRIMARY KEY,
	sport_name VARCHAR(50) UNIQUE NOT NULL,
);
```
``` 
CREATE TABLE teams (
	team_id SERIAL PRIMARY KEY,
	team_name VARCHAR(50) NOT NULL,
	sport_id INT NOT NULL,
	FOREIGN KEY (sport_id) REFERENCES sports(sport_id),
);
```
```
CREATE TABLE players {
	player_id SERIAL PRIMARY KEY,
	first_name VARCHAR(50) NOT NULL,
	last_name VARCHAR(50) NOT NULL,
	age VARCHAR(50) NOT NULL,
	team_id INT NOT NULL,
	FOREIGN KEY (team_id) REFERENCES teams(team_id),
);
```
The text after the datatypes (e.g. `UNIQUE NOT NULL`) are optional [constraints](https://www.postgresql.org/docs/16/ddl-constraints.html#DDL-CONSTRAINTS) that define conditions that must be satisfied by the data.

Here is a link for information on datatypes in PostgreSQL: [https://www.postgresql.org/docs/current/datatype.html](https://www.postgresql.org/docs/current/datatype.html)

Here is a link for more details and examples of how to create a table: [https://www.postgresql.org/docs/current/sql-createtable.html](https://www.postgresql.org/docs/current/sql-createtable.html)


### Table Operations
In SQL, a query is a statement/command used to retrieve or manipulate data in a relational database. To retrieve data from a certain column in a table, you can use the `SELECT` statement and `FROM` clause:
``` 
    SELECT first_name, last_name FROM players;
```
The output of this query is a smaller table that only contains the columns `first_name` and `last_name` of each row from the table `players`.

You can also take the cross product of two or more tables by listing the tables in the `FROM`:
```
    SELECT sport_name, team_name FROM sports, teams;
```
First, this query performs a cross product between `sports` and `teams`. Each row of table `sports` is matched with each row of the table `teams`. Then, it selects the data from the columns `sport_name` and `team_name` of every row present in the newly joined table.

In addition, you can perform filtering on tables:
```
SELECT col1_table1, col2_table2 FROM table1, table2 WHERE col1_table1 > 1;
```
Here it only shows data from the previous table where the value of a row in the column `col1_table1` is greater than 1. This is the syntax for when the table and column names between table 1 and table 2 are unique.

There are many other features of PostgreSQL.

Specifics of the syntax of PostgreSQL can be found in this [link](https://www.postgresql.org/docs/current/sql-syntax.html).

## Setup and PostgreSQL Operations in psycopg2
To start using PostgreSQL in a Python program with psycopg2, ensure you have finished the relevant installations, then follow the instructions below:

1. Create a database in PostgreSQL. This can be done through the command line or pgAdmin. The following steps occur in your python script.
2. Import psycopg2 (see [psycopg2 Installation](#psycopg2-installation-1) above for details).
3. Connect to the new database with connect, eg. `conn = psycopg2.connect("dbname=test user=postgres")`. In this example, *test* is the name of the database that you created, and *postgres* is the default username when you install PostgreSQL. *conn* refers to the Connection (class) you have created, and can be continually referenced until you close the connection, eg. `conn.close()`. It is reccommended to close the connection when you are finished with it.
4. To use your new Connection, you must initialize a Cursor (class) with it. This will allow you to perform PostgreSQL operations on the database. Do this with `cur = conn.cursor()`, where *conn* is our previous Connection, and *cur* is our new Cursor.
5. Using the cursor, you can execute any PostgreSQL command, which will be executed on your database via the settings specified in connect() (see step 3). The PostgreSQL query `SELECT * FROM test;`, for instance, would be executed with `cur.execute("SELECT * FROM test;")`. You can make use of Python's native operations to aid you in your database operations, if you wish. Remember to **never give users direct access to the input of the execute function**. If users can insert text that directly makes its way into the input string, you may be allowing [sql injection](https://www.w3schools.com/sql/sql_injection.asp#:~:text=SQL%20injection%20is%20a%20code,statements%2C%20via%20web%20page%20input.), which could damage or destroy the contents of your database, and leak sensitive information.
6. When you have made your desired changes, use `conn.commit()` to save the changes to your database, and then close your connection with `conn.close()`. If you do not commit the changes, your work will not transfer to your database, but note that if you are only querying data and not making changes, the commit is not required.

psycopg2 can also be used for data processing, with built-in functions such as `fetchone()` and `fetchmany(x)` that return one row and x rows from a query response, respectively. From the example in step 5, after we run `cur.execute("SELECT * FROM test;")`, we can do `row = cur.fetchone()` to save the first row we selected from test to *row*.

These functions can be useful in many situations. For example, if you run a pet store, and possess a PostgreSQL database of adoptable pets, you may have a site that has room to show 4 pets, and an option to show more. Using psycopg2, if you wanted to choose 4 pets in your database, after executing your query with a cursor *cur*, you could call `data = cur.fetchmany(x)`, and then pass your data to your website in whatever way you desire, to be extracted and displayed (Flask has potentially useful psycopg2 integration for this task- see Additional Resourses at the bottom of this page).

For a comprehensive collection of psycopg2 information, including all provided functions and syntax, visit the [offical documentation](https://www.psycopg.org/docs/index.html#).

## Additional Resources
- For further PostgreSQL with psycopg2 examples, and notably examples of full, functional programs, visit this [link](https://wiki.postgresql.org/wiki/Psycopg2_Tutorial).
- For information on using psycopg2 for a flask application, incorporating psycopg2 into your API, visit this [article](https://www.geeksforgeeks.org/making-a-flask-app-using-a-postgresql-database/).
