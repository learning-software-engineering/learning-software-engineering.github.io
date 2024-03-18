# Implement Logging Process to MySQL for Functions

## Introduction

In this guide, we'll explore how to implement a logging process for software functions into a MySQL database. Logging is crucial for monitoring, debugging, and security purposes in software engineering. We'll cover the basics, the setup required, and provide a step-by-step example.

## Prerequisites

- Basic knowledge of programming (Python used in examples)
- Access to a MySQL database
- Familiarity with SQL queries

## Step 1: Setting Up Your Environment

Ensure you have Python and MySQL installed on your system. You'll also need the `mysql-connector-python` package for Python.

```bash
pip install mysql-connector-python
```

## Step 2: Create a Logging Table in MySQL

The `logs` table is essential for storing application log messages, which are crucial for debugging, monitoring application health, and understanding user actions.

Execute the following SQL query in your MySQL database to create a table for logging:

```sql
CREATE TABLE logs (
    id INT AUTO_INCREMENT PRIMARY KEY,
    timestamp TIMESTAMP DEFAULT CURRENT_TIMESTAMP,
    level VARCHAR(10),
    message TEXT
);
```

<img width="694" alt="logs_table" src="https://github.com/learning-software-engineering/learning-software-engineering.github.io/assets/90298039/76e95152-0812-4b1b-8338-2a9ddbf26e0e">

- **id** (INT): An auto-incremented integer serving as the primary key for each log entry.
- **timestamp** (TIMESTAMP): The date and time when the log entry was created, automatically set to the current timestamp.
- **level** (VARCHAR): A string indicating the severity of the log, such as INFO, WARNING, or ERROR.
- **message** (TEXT): The actual log message text, detailing the event or error reported.

## Step 3: Implementing Logging in Python

### Define the Logger

Create a Python file, e.g., logger.py, and define a logger and a handler to insert logs into MySQL.

```python
import logging
import mysql.connector
from mysql.connector import Error

class MySQLHandler(logging.Handler):
    def __init__(self, config):
        super().__init__()
        self.connection = mysql.connector.connect(**config)
        self.cursor = self.connection.cursor()

    def emit(self, record):
        try:
            log_entry = self.format(record)
            self.cursor.execute("INSERT INTO logs (level, message) VALUES (%s, %s)", (record.levelname, log_entry))
            self.connection.commit()
        except Error as e:
            print("Error logging to MySQL", e)
```

### Configure the Logger

Configure the logger with the MySQL handler.

```python
logger = logging.getLogger(__name__)
logger.setLevel(logging.INFO)

config = {
    'host': 'your_database_host',
    'database': 'your_database_name',
    'user': 'your_username',
    'password': 'your_password'
}

mysql_handler = MySQLHandler(config=config)
logger.addHandler(mysql_handler)

formatter = logging.Formatter('%(asctime)s - %(levelname)s - %(message)s')
mysql_handler.setFormatter(formatter)
```

## Usage Example with the `users` Table

In this example, we have a `users` table in our MySQL database designed to store user information such as IDs, names, and email addresses. 
The table structure is as follows:

- **id** (INT): A unique identifier for each user, auto-incremented.
- **name** (VARCHAR): The name of the user.
- **email** (VARCHAR): The user's email address, which is unique across all users.

### Creating the `users` Table

First, ensure that your MySQL database contains the `users` table. Use the following SQL query to create it if necessary:

```sql
CREATE TABLE users (
    id INT AUTO_INCREMENT PRIMARY KEY,
    name VARCHAR(100) NOT NULL,
    email VARCHAR(100) NOT NULL UNIQUE
);
```

<img width="554" alt="users_table" src="https://github.com/learning-software-engineering/learning-software-engineering.github.io/assets/90298039/7e46d8ac-a9cb-454e-8543-7ae445e042c6">

### Inserting Sample Data

Insert some sample data into the `users` table to work with:

```sql
INSERT INTO users (name, email) VALUES ('Alice Smith', 'alice@example.com');
INSERT INTO users (name, email) VALUES ('Bob Jones', 'bob@example.com');
```

<img width="354" alt="users_sample_data" src="https://github.com/learning-software-engineering/learning-software-engineering.github.io/assets/90298039/8fff4603-2cbf-417d-afbe-32f6f2a86dee">

### The `get_user_info` Function

The `get_user_info` function is designed to retrieve a user's information from the database given their user ID. 
It uses logging to indicate the function's outcome, such as successful information retrieval, attempts to retrieve non-existent users, and database connection errors.

### Python Implementation

Below is the updated Python script that includes the `get_user_info` function:

```python
import logging
import mysql.connector
from mysql.connector import Error

# Configure the logger and MySQLHandler as previously described

def get_user_info(user_id):
    """Retrieves user information by user_id from the database."""
    try:
        conn = mysql.connector.connect(**config)
        cursor = conn.cursor()
        cursor.execute("SELECT * FROM users WHERE id = %s", (user_id,))
        user_info = cursor.fetchone()
        conn.close()

        if user_info:
            logger.info(f"Retrieved information for user ID {user_id}: {user_info}")
            return user_info
        else:
            logger.warning(f"User with ID {user_id} not found.")
            return None
    except Error as e:
        logger.error(f"Error connecting to MySQL database: {e}")
        return None

# Example usage
user_id = 1  # Example user ID
user_info = get_user_info(user_id)
```

### Explanation

This script attempts to retrieve information for a user by their ID. It logs:

- An **info** level message if the information is successfully retrieved,

https://github.com/learning-software-engineering/learning-software-engineering.github.io/assets/90298039/bd2777b4-93d8-490a-88fe-eacf04d570a1

- A **warning** if no user matches the provided ID, and

https://github.com/learning-software-engineering/learning-software-engineering.github.io/assets/90298039/fadc999f-04c5-4488-89a4-60fabdcb1f59

- An **error** if there is a problem connecting to the database.

https://github.com/learning-software-engineering/learning-software-engineering.github.io/assets/90298039/66d5602e-b31b-4558-8098-e2ff8d6cc741

This approach demonstrates practical logging usage within an application, providing insights into operational status and issues.

## Conclusion

Implementing a logging process into MySQL allows developers to effectively monitor and debug their applications. 
By following the steps outlined above, you can set up a robust logging system tailored to your project's needs.

## References

- [MySQL Connector/Python Developer Guide](https://dev.mysql.com/doc/connector-python/en/)
- [Logging facility for Python — Python 3.12.2 documentation](https://docs.python.org/3/library/logging.html)

This document is structured to facilitate readability and understanding, featuring code blocks for SQL, bash, and Python 
to illustrate the setup and implementation process for logging to MySQL. Remember to adjust the configuration details to match your environment.









