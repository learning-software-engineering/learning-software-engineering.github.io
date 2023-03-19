# Learning MySQL

## Introduction

The following is an introduction to MySQL with some resources to get started. *This article assumes that the reader has some knowledge about Structured Query Languages (SQL). For more information about SQL in general, you can check out [this link](https://www.postgresqltutorial.com/postgresql-tutorial/postgresql-vs-mysql/)*. A relational database management system (RDBMS) which is used to implement databases for any general application. MySQL is one of the most popular DBMSs because it is flexible, secure, and has high performance. For more details, [click here](https://www.hostinger.com/tutorials/what-is-mysql).

## MySQL vs other DBMSs

When choosing a database management system, there may be a lot of options. here are some comparisons between the most popular ones:

* Vs. PostgreSQL
  * Postgres is more geared towards applications that require complex queries and large amounts of data since it boasts many features that are not present in MySQL. Some of these features include [table inheritance](https://www.postgresql.org/docs/7.2/inherit.html) and [function overloading](https://www.postgresql.org/docs/current/xfunc-overload.html). For a more detailed comparison you can check out [this link](https://www.integrate.io/blog/postgresql-vs-mysql-which-one-is-better-for-your-use-case/).
* Vs. MongoDB
  * MongoDB is a NoSQL database, meaning that it does not follow SQL rules and schemas and instead uses JSON rules to store data. Therefore it is more flexible. It is also geared towards write performance and is better for [real time applications](https://www.simplilearn.com/tutorials/mongodb-tutorial/mongodb-vs-mysql#:~:text=MySQL%20is%20an%20excellent%20choice,and%20other%20types%20of%20applications.)

## MySQL client installation and basic operations

The following is a summary from [this guide](https://dev.mysql.com/doc/mysql-getting-started/en/) which has many details, but here are the following steps:
1) Download the client <br />
  i) **Linux** <br />
    Follow the instructions on this [this link](https://dev.mysql.com/doc/refman/8.0/en/linux-installation.html). For users using Debian or Ubuntu, use the [APT documentation here](https://dev.mysql.com/doc/mysql-apt-repo-quick-guide/en/#apt-repo-fresh-install) and follow the 3 steps. <br />
  ii) **Windows** <br />
    Follow the instructions on [this link](https://dev.mysql.com/doc/refman/5.7/en/windows-installation.html#windows-installation-simple) which provides 3 steps in order to complete this step using an installer. <br />
  iii) **macOS** <br />
    Follow steps 1-8 from [this link](https://dev.mysql.com/doc/refman/8.0/en/macos-installation-pkg.html) which shows you how to nagivate the Installer Wizard.
2) Connect to the MySQL server using the mysql client <br />
  i) **Linux Based Systems** <br />
    Enter the following in the command line terminal <br />
    > $`>` mysql -u root -p <br />
  ii) **Windows** <br />
    Go to **Start, All Programs, MySQL, MySQL 5.7 Command Line Client (or MySQL 8.0 Command Line Client, respectively)**
3) Run SQL statements to create schemas and run operations. Here are some examples
  * Creating a new database.  Use a [CREATE DATABASE](https://dev.mysql.com/doc/refman/8.0/en/show-databases.html) statement
  * Create a table with a [CREATE TABLE](https://dev.mysql.com/doc/refman/8.0/en/create-table.html) statement
  * Adding records into a table using [INSERT...VALUES](https://dev.mysql.com/doc/refman/8.0/en/insert.html) statement
  * Use a [DELETE](https://dev.mysql.com/doc/refman/8.0/en/delete.html) statement to delete a record from a table

## MySQL integration

There are many environments that can integrate a MySQL database. Here is how to do it in Node.js and Python

### MySQL database connection to Node.js

Assuming that npm and node is installed (click here for [npm instructions](https://docs.npmjs.com/downloading-and-installing-node-js-and-npm), use the following commands in the terminal
* `npm init -y`
* `npm install mysql`
* In your mysql client use the database command `CREATE DATABASE databaseName;` to create a database to connect to
* In your .js file, use `import 'mysql';`
* Use `let connection = mysql.createConnection({host: 'localhost', user: 'root', password: '', database: 'databaseName'});` in the .js file to connect to the database server. The host, user, and password parameters can be changed to your specific usage. 
* Use the form `connection.connect(function(err) {...});` to connect to the database, where the ... represents your error checking method incase the connection fails. 
* To close the connection, use the form `connection.end(function(err) {...});` where ... represents the error checking method of your choice. 

For more detailed steps, check out [this link](https://www.mysqltutorial.org/mysql-nodejs/connect/)




