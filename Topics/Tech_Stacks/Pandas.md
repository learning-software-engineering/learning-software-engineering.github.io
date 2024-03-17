
# Introduction to Pandas in Python

## Table of Contents
### [Introduction](#introduction)
### [Prerequisites](#prerequisites)
### [Installation](#installation)
### [Basic Concepts](#basic-concepts)
### [Reading Data](#reading-data)
### [Data Manipulation](#data-manipulation)
### [Data Analysis and Visualization](#data-analysis-and-visualization)
### [Best Practices](#best-practices)
### [References](#references)

##  Introduction
Pandas is an open-source Python library for data analysis and manipulation. It is one of the most powerful and popular libraries in all of Python; widely used by the Python community for its ability to provide highly efficient, easy-to-use, and extensive data structures and data analysis tools. As well as its seamless integration with other libraries. This wiki page will serve as a brief introduction to the Pandas library.

## Prerequisites
To start with pandas, Python must already be installed on your machine. The Pandas library officially only supports Python version 3.9 or newer

## Installation
To install Pandas once Python is on your machine, run the following pip command:
```bash
pip3 install pandas
```

To get started, open up a fresh Python file and import the library. It is common practice to import pandas under the alias "pd" as seen below:
```python
import pandas as pd
```

And now you're ready to use Pandas!

## Basic Concepts
The two main Pandas data structures are the Series and the DataFrame.

### Series
A Series is a one-dimensional array that can store any data type (but all its elements must have the same data type). It can be thought of as a column in a spreadsheet. Each element in a series has an index much like the standard Python list. These indexes are customizable as long as the labels are of hashable datatypes.

Example of creating a series:
```python
import pandas as pd

data = pd.Series([0, 2, 4, 6])
```

Example of assigning custom indexes:
```python
data = pd.Series([0, 2, 4, 6], index=['a', 'b', 'c', 'd'])
```

### DataFrame
A DataFrame on the other hand is a two-dimensional array, comparable to an entire spreadsheet. Both the rows (indexes) and columns are customizable as long as the labels are of hashable datatypes.

Example of creating a DataFrame, by first creating a dictionary and then converting it to a DataFrame (note: the lists must all be of equal length):
```python
import pandas as pd

data = {
    'Name': ['Ryan', 'Sean', 'Jacob'],
    'Age': [20, 74, 29],
    'Favorite Food': ['Pizza', 'Pasta', 'Burgers']
}

df = pd.DataFrame(data)
```

Example of assigning custom row and column labels:
```python
df.index = ['Student 1', 'Student 2', 'Student 3']
df.columns = ['First Name', 'Age', 'Favorite Food']
```

## Reading Data
Pandas has many functions that allow the user to import data from different filetypes into the DataFrame structures:

Reading from CSV files:
```python
df = pd.read_csv('path_to_csv_file/file.csv')
```

Reading from Excel files:
```python
df = pd.read_excel('path_to_excel_file/file.xlsx')
```

Reading from JSON files:
```python
df = pd.read_json('path_to_excel_file/file.json')
```

Examples of other supported files are HTML and SQL files which are read from using the read_html and read_sql functions respectively.

The data imports can also be customized in many different ways. For example, you can handle empty values with the na_values parameter and declare the column data types using the dtype parameter. This will be covered further in the Data Manipulation section.

## Data Manipulation
Pandas offers a large variety of functionalities for data manipulation that help users easily clean and transform their data for analysis and visualization.

### Selecting Rows & Columns
Selecting Rows by their index label (loc):
```python
# single row
row = df.loc['label']

# multiple rows
rows = df.loc[['label1', 'label2']]
```
Selecting Rows by their index position (iloc):
```python
# single row
row = df.iloc[0]

# multiple rows
rows = df.iloc[0:5]  # first five rows, behaves just like list indexing in python
```

Selecting Columns:
Selecting Columns by their index label:
```python
# single col
column = df['col_name']

# multiple cols
columns = df['col_name1', 'col_name2']
```

Selecting Columns by their index label:
```python
# first col
column = df.iloc[:, 0]

# multiple cols
columns = df.iloc[:, 0:3]  # first 4 columns
```

### Adding/Removing Columns & Rows
Adding Columns:
```python
# adding a single column
df['Field'] = 'Marketing'

# add a column derived from another
df['Yearly Salary'] = df['Monthly Salary'] * 12
```

Removing Columns:
```python
# remove one col
df.drop('Department', axis=1, inplace=True)

# remove multiple
df.drop(['Annual Salary', 'OtherColumn'], axis=1, inplace=True)
```

Removing Rows:
```python
# remove one row
df = df.drop('label')

# remove multiple
df = df.drop(['label1', 'label2'])
```

### Filtering Data & Conditional Operations
Filtering selecting rows/columns that abide by one or more conditions:
```python
# rows where age is greater than 65
senior_citizens = df[df['Age'] > 65]

# rows where age is greater than 65 and the birthplace is California
senior_californians = df[(df['Age'] > 65) & (df['Birthplace'] == 'California')]
```

We can also conditionally modify DataFrames:
```python
# remove rows where a col's val doesn't abide by a condition
df = df[df['Age'] <= 18]

# remove rows with multiple conditions (~ means negation)
df = df[~((df['Age'] < 18) | (df['Age'] > 65))]
```

### Cleaning & Sorting Data
Sorting values
```python
# sort by one column
df.sort_values(by='Age', inplace=True)

# sort by multiple columns
df.sort_values(by=['Age', 'Height'], ascending=[True, False], inplace=True)
```

Dealing with empty values using na_values:
```python
na_values = ['', 'Null']

# tells pandas to treat strings with these values as NaN (not a number)
df = pd.read_csv('path_to_csv_file/file.csv', na_values=na_values)
```




