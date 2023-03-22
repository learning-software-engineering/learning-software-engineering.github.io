# Learning PostgreSQL and psycopg2

### Prerequisites
Before learning about PostgreSQL and psycopg2, ensure that you have knowledge about the following:
- [Python](https://www.python.org/): High level general purpose programming language.
- Relational Algebra and Database Theory (e.g. What is a relation? What is a query?)

### Introduction
PostgreSQL is an open-source DBMS. As the name states, PostgreSQL is a relational DBMS based on relations and queries and is great for dealing with large amounts of data and complex queries. It's also good for referencing data quickly and allowing the user to have some flexibility in how they want to represent their data. Furthermore, PostgreSQL supports table inheritance and function overloading.

pyscopg2 is an adapter for Python that allows you to easily integrate PostgreSQL into your program. It's commonly used with other Python libraries like Flask, which allows you to use a PostgreSQL database in you application easily.

### PostgreSQL and psycopg2 installation
The following link is to download PostgreSQL onto your computer: https://www.postgresql.org/download/ . This link also shows the different versions of PostgreSQL to match your computer. Follow the instructions after downloading. For your convenience, here is the links to download the installer for PostgreSQL on different OS:
- Windows: https://www.postgresql.org/download/windows/
- MacOS: https://www.postgresql.org/download/macosx/
- Linux: https://www.postgresql.org/download/linux/

Once installed, you can create a database, relation, and tables with the PostgreSQL client called "pgAdmin". You can also perform queries on relations and tables through its query tool. More information on how to use pgAdmin can be found from this [link](https://www.pgadmin.org/docs/pgadmin4/6.21/index.html).


To install psycopg2, you can use pip to install its funcionality by using the command:
"pip install psycopg2". After installing this in your desired directory, you can import psycopg2 into your python files and perform PostgreSQL queries very intuitively.

### Basic Operations
A very very quick and basic runover of PostgreSQL.

To select data from a certain column in a table, you can use a query like:
``` 
    SELECT column1, column2 FROM table_name;
```
This gives you a smaller table that only contains column1 and column2 from your selected table in your relation. 

You can also merge two different tables by changing the FROM clause to contain 2 tables:
```
    SELECT col1_table1, col2_table2 FROM table1_name, table2_name;
```
This operation, first, performs a cross product between table1 and table2, where every row of one table is matched with every other row the other table. Then it selects the data present in the new cross products table from columns col1_table1 and col2_table2.

In addition, you can perform filtering on tables:
```
SELECT col1_table1, col2_table2 FROM table1_name, table2_name WHERE col1_table1 > 1;
```
Here it only shows that data from the previous table where the value of col1_table1 is greater than 1. This is the syntax for when the table and column names between table 1 and table 2 are unique.

Specifics of syntax of PostreSQL can be found in this [link](https://www.postgresql.org/docs/current/sql-syntax.html).

As a quick runover, to start using PostgreSQL in you Python script, you must first setup the psycopg2 module in the Python file. 

This can be done by:

1. 

Specifics of syntax and module use of psycopg2 can be found in this [link](https://www.psycopg.org/docs/usage.html#passing-parameters-to-sql-queries). The syntax that involves making queries in psycopg2 is the same as PostgreSQL.



### psycopg2 integration

Here is a link on operations and commands to use psycopg2 in Python:
https://pynative.com/python-postgresql-tutorial/#h-python-postgresql-database-connection

### Additional Resources