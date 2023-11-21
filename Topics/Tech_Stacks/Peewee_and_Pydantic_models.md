# Python Peewee and Pydantic Models Tutorial

## Table of Contents
1. [Introduction](#introduction)
2. [What is Peewee?](#what-is-peewee)
3. [What is Pydantic?](#what-is-pydantic)
2. [Installation](#installation)
2. [Setting Up Peewee Models](#setting-up-peewee-models)
3. [Peewee Models and Field Types](#peewee-models-and-field-types)
    - [CharField](#charfield)
    - [IntegerField](#integerfield)
    - [FloatField](#floatfield)
    - [DecimalField](#decimalfield)
    - [BooleanField](#booleanfield)
    - [DatField and TimeField](#datefield-and-timefield)
    - [ForeignKeyField](#foreignkeyfield)
5. [Defining Keys in Peewee Models](#defining-keys-in-peewee-models)
    - [Primary Key](#primary-key)
    - [Composite Key](#composite-key)
    - [Indexing](#indexing)
    - [Constraints](#constraints)
3. [Using Pydantic for Data Validation](#using-pydantic-for-data-validation)
4. [CRUD Operations with Peewee and Pydantic Validation](#crud-operations-with-peewee-and-pydantic-validation)
5. [Conclusion](#conclusion)

## Introduction
Peewee is a lightweight Python ORM (Object-Relational Mapping). Essentially, this creates a bridge beteween object-oriented programs. Pydantic on the other hand is a data validation and parsing tool. My group combine these technologies and allowed us to improve database interactions, data validation, and general data management in our backend.

## What is Peewee?
Peewee, as previously said, is an ORM that provides a simple and expressive API for working with backend databases. It supports a number of database backends, including SQLite, MySQL, and PostgreSQL; in our case, my group utilized it with a Postgresql database. Peewee simplified our database activities by allowing us to construct models by modeling database tables, making it easier to do CRUD operations without having to write our query statements in SQL; instead, we can write them in Python.

## What is Pydantic?
Pydantic ensures that data follows a given structure; in my group's instance, we ensured that our response models from API calls are of a specific kind. This is critical when we wish to specify our anticipated values from data so that they may be validated and worked with more easily. This was extremely useful in web development, API handling, and other situations where data integrity was critical.

## Installation
First, let's install the necessary packages, this can be done through pip in your virtual environment or poetry, our group opted for using poetry as a package manager:

```bash
pip install peewee pydantic
```

## Setting Up Peewee Models
Peewee models represent tables in your database. Create a new file, e.g., models.py, and define your models:

```python
from peewee import Model, SqliteDatabase, CharField, IntegerField

db = SqliteDatabase('example.db')  # Change 'example.db' to your preferred database name

class Person(Model):
    name = CharField()
    age = IntegerField()

    class Meta:
        database = db

db.connect()
db.create_tables([Person])
```
This short example defines a Person model with a `name` field of type `CharField` and an `age` field of type `IntegerField`. Lets learn about other fields and models that you can create with them!

## Peewee Models and Field Types
There are lot of fields within Peewee that can be used to specify the data type of each column of your databse tables. Let's look at some common field types in Peewee that you are most likely going to use:

### CharField
The `CharField` is often used for short to medium strings, such as names and titles. Here is an example usage:

```python
class Person(Model):
    name = CharField(max_length=100)
```

### IntegerField
The `IntegerField` represents a 32-bit signed integer, which is commonly used for storing whole numbers. Example usage:

```python
class Person(Model):
    age = IntegerField()
```

### FloatField
The `FloatField` is used for storing floating-point numbers. If you need to store numbers with decimal points, use this field type. Example usage:

```python
class Product(Model):
    price = FloatField()
```

### DecimalField
Similar to `FloatField`, the `DecimalField` is used for storing decimal numbers with fixed precision. It's a good choice when accuracy is crucial, such as when dealing with financial data. Example usage:

```python
class Order(Model):
    total_amount = DecimalField(max_digits=10, decimal_places=2)
```
### BooleanField
The `BooleanField` represents a boolean value (True or False). It's suitable for fields that indicate a binary state. Example usage:

```python
class Task(Model):
    completed = BooleanField()
```

### DateField and TimeField
The `DateField` and `TimeField` are used for storing dates and times, respectively. Example usage:

```python
class Event(Model):
    event_date = DateField()
    event_time = TimeField()
```

### ForeignKeyField
The `ForeignKeyField` is used to make a many-to-one relationship between two models. It's used when a field in one table depends on the primary key in another table. The `backref` allows you to access properties associated with the Foreign Key, in the case below. We can access the comments associated with a post using `comments` attribute. Example usage:

```python
class Comment(Model):
    text = CharField()
    post = ForeignKeyField(Post, backref='comments')
```

These are just a few examples of the field types provided by Peewee. But now, you might be wondering we defined Foregin Keys, but how do we define Primary Keys of a database? Its similar to how we define Foreign Key Fields, but there are a few more features and thus this garners its own section below.

## Defining Keys in Peewee Models
In any relational database, keys play a crucical role in defining the relationships between tables and ensuring the integrity of the database itself. There are Foreign Keys, which already has be briefly outlined above. But peewee also supports Primary Keys and Composite Keys.

### Primary Key
The Primary Key helps uniquely identifies each record in a table. In Peewee, you can designate a primary key to a field using the `PrimaryKeyField` or, by default, if you don't put anything as a `PrimaryKeyField` Peewee automatically creates an integer primary key called id.

Using `PrimaryKeyField`
```python
class Person(Model):
    person_id = PrimaryKeyField()
    name = CharField()
```

Using the Default Integer Primary Key
```python
class Person(Model):
    name = CharField()
```

### Composite Key
A Composite Key involves using multiple fields together as a unique identifier. Peewee supports composite keys by combining multiple fields within a `PrimaryKeyField`.

```python
class ProductVariant(Model):
    product = ForeignKeyField(Product)
    variant_name = CharField()
    color = CharField()

    class Meta:
        primary_key = CompositeKey('product', 'variant_name', 'color')
```
In this example, `product`, `variant_name`, and `color` together form a composite primary key.

### Indexing
You can also define indexes on fields to improve query performance. Use the `index` parameter in your field definition:

```python
class User(Model):
    username = CharField(index=True)
    email = CharField(index=True)
```
This creates indexes on the `username` and `email` fields.

### Constraints
Peewee allows you to define constraints on your fields, such as `unique` constraints, which ensure that no two records have the same value for a particular field:

```python
class User(Model):
    username = CharField(unique=True)
    email = CharField(unique=True)
```
This enforces uniqueness for both `username` and `email`.

As previously stated, keys and constraints help enforce relationships between relational database tables. There are a lot of different upsides to designing good databases as it could ensure data integrity, and improve query performance in schemas. Thus, it is worthwhile to spend time designing the relational database tables within your application! What I have covered here is just the tip of the iceberg! You can learn more about keys [here](https://docs.peewee-orm.com/en/latest/peewee/models.html#primary-keys-composite-keys-and-other-tricks).

## Using Pydantic for Data Validation
Next, create a Pydantic model for data validation. In a file like schemas.py:

```python
from pydantic import BaseModel

class PersonSchema(BaseModel):
    name: str
    age: int
```

Here, `PersonSchema` mirrors is exactly the same as the fields of the Peewee model. After, this Pydantic will ensure that the data you receive or send adheres to the specified structure!

## CRUD Operations with Peewee and Pydantic Validation
Now, let's perform CRUD (Create, Read, Update, Delete) operations using Peewee. In a new file, e.g., crud_operations.py:

```python
from models import Person, db
from schemas import PersonSchema

# Create
def create_person(person_data) -> PersonSchema:
    # creates instance of the PersonSchema, using double astricks syntax to unpack contents
    person_schema = PersonSchema(**person_data)
    # convert pydantic model into a dictionary, ensuring data conforms to expected structure of Pydantic model
    validated_data = person_schema.dict()
    person = Person.create(**validated_data)
    return PersonSchema(**person.__dict__)  # Return as PersonSchema instance

# Read
def get_person(person_id) -> PersonSchema:
    person = Person.get_by_id(person_id)
    return PersonSchema(**person.__dict__)  # Return as PersonSchema instance

# Update
def update_person(person_id, new_data):
    person = Person.get_by_id(person_id)
    
    # Validate and update data
    person_data = PersonSchema.from_orm(person).dict()
    updated_data = {**person_data, **new_data}
    updated_person = PersonSchema(**updated_data)
    
    # Save the updated data
    person.name = updated_person.name
    person.age = updated_person.age
    person.save()

# Delete
def delete_person(person_id):
    person = Person.get_by_id(person_id)
    person.delete_instance()

# Close the database connection when done
db.close()
```
This script demonstrates basic CRUD operations in Peewee alongside with Pydantic validation!

## Conclusion
You can now set up Peewee models, used Pydantic for data validation, and implemented basic CRUD operations. If you want to find out more about these two peices of software, take a look at [Peewee docs](https://docs.peewee-orm.com/en/latest/index.html) and [Pydantic docs](https://docs.pydantic.dev/latest/).