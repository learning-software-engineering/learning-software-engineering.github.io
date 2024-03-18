
# Introduction to Pandas in Python

## Table of Contents
- [Introduction](#introduction)
- [Prerequisites](#prerequisites)
- [Installation](#installation)
- [Basic Concepts](#basic-concepts)
- [Reading Data](#reading-data)
- [Data Manipulation](#data-manipulation)
- [Data Analysis](#data-analysis)
- [Data Visualization](#data-visualization)
- [Comparisons to Other Data Processing Tools](#comparisons-to-other-data-processing-tools)
- [Conclusion](#conclusion)
- [References](#references)

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

Reading from SQL files:
We can use a python SQL toolkit like SQLAlchemy in conjunction with Pandas to query results into DataFrames
```python
import pandas as pd
from sqlalchemy import create_engine

# connect to db
engine = create_engine('postgresql+psycopg2://path_to_db/file.db')

# query results into data frame
df = pd.read_sql("SELECT * FROM table", con=engine)
```

There are several other file types that can be read from in Pandas such as plain text, HTML, and PDFs.

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
df['field'] = 'marketing'

# add a column derived from another
df['yearly salary'] = df['monthly salary'] * 12
```

Removing Columns:
```python
# remove one col
df.drop('employee12', axis=1, inplace=True)

# remove multiple
df.drop(['yearly salary', 'marketing'], axis=1, inplace=True)
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

## Data Analysis

.describe() outputs a description of the statistics of your DataFrame including median, mean, and standard deviation
```python
stats = df.describe()
```

.corr() outputs the correlations between pairs of columns in your DataFrame
```python
correlation_table = df.corr()
```

.groupby() method allows to aggregate data into groups and thus carry out operations on these groups individually
```python
group_means = df.groupby('age').mean()
```

.value_counts() counts the mode (number of occurrences) of each value in a column
```python
data = {'colour': ['Red', 'Red', 'Blue', 'Red']}
df = pd.DataFrame(data)
print(df['colour'].value_counts())

'''
Returns:
Red 3
Blue 1
'''
```

## Data Visualization
Libraries like Matplotlib and Seaborn are frequently used in conjunction with Pandas to visualize data. We will not delve deep into these libraries in this guide, but below is a simple example to demonstrate how Pandas can be used with Matplotlib to visualize data. I encourage you to look further into each library's vast capabilities.

```python
import matplotlib.pyplot as plt
import pandas as pd

# monthly sales dictionary for two products
data = {
    'Month': ['January', 'January', 'February', 'February', 'March', 'March',
              'April', 'April', 'May', 'May'],
    'Product': ['Product A', 'Product B', 'Product A', 'Product B', 'Product A', 'Product B',
                'Product A', 'Product B', 'Product A', 'Product B'],
    'Sales': [150, 150, 200, 50, 200, 100, 100, 250, 300, 200]
}

# converting this dictionary to a data frame
df = pd.DataFrame(data)
months = ['January', 'February', 'March', 'April', 'May']
a_sales = df[df['Product'] == 'Product A']['Sales']  # selecting the sales of product A
b_sales = df[df['Product'] == 'Product B']['Sales'] # selecting the sales of product B

# LINE PLOT


plt.figure(figsize=(10, 5))  # setting the size of the figure
plt.plot(months, a_sales, label='Product A')
plt.plot(months, b_sales, label='Product B')

# line plot styling
plt.title('Monthly Sales Trends')
plt.xlabel('Month')
plt.ylabel('Sales')
plt.legend()
plt.show()


# BAR CHART

# calculate average sales
avg_sales = df.groupby('Product')['Sales'].mean()

plt.figure(figsize=(10, 5))
plt.bar(avg_sales.index, avg_sales.values, color=['red', 'blue'])

# bar chart styling
plt.title('Average Sales by Product')
plt.xlabel('Product')
plt.ylabel('Average Sales')
plt.show()
```

Generated Line Plot:
![lineplot](https://github.com/learning-software-engineering/learning-software-engineering.github.io/assets/55326695/0acb6bc5-599d-44ff-8d6d-36bb6436dd01)


Generated Bar Chart:
![barchart](https://github.com/learning-software-engineering/learning-software-engineering.github.io/assets/55326695/4f9a3855-7d3f-4930-a238-a65eb6437ecb)

## Comparisons to Other Data Processing Tools
### Pandas vs R
- Language: Pandas is a library in Python, while R is its own programming language specifically designed for statistical computing
- Syntax and Usage: R's syntax is made for statistical analysis and can be more intuitive for statistical tasks. 
- Use Cases: Pandas is part of Python, making it better for integration with a variety of solutions built on Python like web apps and machine learning algorithms.
### Pandas vs NumPy
- Functionality: NumPy is best at numerical and mathematical computations, especially on arrays, Pandas is built on top of NumPy but provides more tools for data cleaning, transformation, and analysis.
- Use Cases: NumPy is better for low level mathematical tasks, where the data is numerical and mostly homogenous. Pandas is designed for higher-level data manipulation and analysis, including when dealing with complex, real world datasets that include missing values, need to be cleaned, or grouped.
- Efficiency: NumPy is fast for math operations because it does calculations all at once across its rows. Pandas is a bit slower because it has more overhead for its extra features like handling missing data or letting you label data.

## Conclusion
There are endless possibilities with this library and this page is only a brief introduction to the library. I encourage you to check out the links in the references section to explore this library further and delve into more advanced topics like windowing operations, time series analysis, and enhancing performance for big datasets. Also using Pandas with other libraries like Matplotlib, Seaborn, and even machine learning libraries like Scikit-learn will open up many more data analysis doors.

Thanks for reading!

## References
https://pandas.pydata.org/docs/user_guide/index.html

https://www.w3schools.com/python/pandas/default.asp

https://www.datacamp.com/tutorial/pandas







