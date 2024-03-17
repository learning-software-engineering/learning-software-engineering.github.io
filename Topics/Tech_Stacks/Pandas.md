
# Introduction to Pandas in Python

## Table of Contents
### [Introduction](#introduction)
### [Prerequisites](#prerequisites)
### [Installation](#installation)
### [Basic Concepts](#basic-concepts)
### [Reading Data](#basic-concepts)
### [Data Manipulation](data-manipulation)
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
A DataFrame on the other hand is a two-dimensional array where each index represents a row, comparable to an entire spreadsheet. Both the rows (indexes) and columns are customizable as long as the labels are of hashable datatypes.

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



