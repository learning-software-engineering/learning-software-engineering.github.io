# Learning NumPy

## Table of Contents

### [Introduction](#introduction-1)

### [Set Up](#set-up-1)

### [Array Basics](#array-basics-1)

### [Matrices and Operations](#matrices-and-operations-1)

### [Additional Resources](#additional-resources-1)

## Introduction
This is a short introduction to NumPy, for people looking for a basic overview of the library before doing further research into how to use it, which can be done through visiting some of the additional resources linked at the bottom of this page. Specifically, all the topics covered on this page as well as many more are discussed in both the official beginners guide and the video tutorial linked resources.
NumPy is a Python library which provides users with new data structures which represent arrays of one or more dimensions, as well as a variety of methods for different mathematical operations which chain together effectively. It is designed for use in engineering, statistical, mathematical, as well as any other computing and/or scientific contexts where complicated operations are to be conducted on data sets of various shapes efficiently.

## Set Up
In order to use NumPy, it needs to be installed just like any other Python library. The most basic way this can be done is having Python already installed and installing NumPy through the shell using pip or Anaconda:
Using pip:
```bash
> pip install numpy
```
Using Anaconda:
```bash
> conda install numpy
```
For more detailed instructions on ways to install NumPy, there is a linked additional resource at the bottom of the page labelled 'Installing NumPy'.

Finally, in order to use NumPy resources in your Python code, it is important to import the library. The general convention is to give the package the name 'np' in the import as a shorthand, however it is technically not necessary. Code blocks in this page will be written assuming that the import is done as is below:
```py
import numpy as np
```

## Array Basics
The most basic object to create in NumPy is the array, which is similar to the default Python list, however it is designed to be more memory efficient, reliable, and it comes with a variety of additional methods. An array can be created with an inputted Python list:
```py
firstArray = np.array([4, 2, 3, 1, 5])
print(firstArray) # '[4 2 3 1 5]'

# Index the array in the same way as you would a list.
# Negative indices work in the same way as well.
print(firstArray[2]) # '3'
print(firstArray[-1]) # '5'

# Slice the array in the same way as you would a list.
print(firstArray[1:3]) # '[2 3]'

# Arrays also come with min, max, sum, and count (called size instead of count).
print(firstArray.min()) # '1'
print(firstArray.max()) # '5'
print(firstArray.sum()) # '15'
print(firstArray.size) # '5'

# Arrays can be concatenated in the same way as lists, using the following method:
first = np.array(['a', 'b', 'c'])
second = np.array(['d', 'e', 'f'])
concatenated = np.concatenate((first, second))
print(concatenated) # '['a' 'b' 'c' 'd' 'e' 'f']'
```

An array can also be created with fixed values, such as 0's or 1's, or if speed is a concern, then there is a method to create an array with random values at each index (it is important to remember this if using NumPy's 'empty()' function):
```py
# Create arrays with inputted size attributes. The default type of each element in these arrays is a 64-bit float, which is why 0 appears as '0.'.
# Array with random values in each index.
empty = np.empty(3)

# Array with zeroes/ones in each index.
zeroArray = np.zeros(3)
oneArray = np.ones(3)
print(zeroArray) # '[0. 0. 0.]'
print(oneArray) # '[1. 1. 1.]'
```

It is important to mention that arrays must contain elements of the same type. There will be an example below showcasing what happens when given a list of various types as an argumen to the array constructor. 
Additionally, arrays can be constructed as a range (similar to Python's 'range' function), which can also be defined as a range spaced linearly. 
Finally, as mentioned above, arrays are defined by default to contain elements of the type np.float64, which is a 64-bit floating point number. When creating an array, a pre-defined NumPy data type can be passed in to define the type of the array elements:
```py
# Creating this array will make each element turn into a string:
variety = np.array([True, 2, 'c'])
print(variety) # '['True' '2' 'c']'

# Creating a range array
zeroToTwo = np.arange(3)
print(zeroToTwo) # '[0 1 2]'

# Creating a linearly spaced array
zeroToEightEven = np.linspace(0, 8, 5) # This means to divide the range from 0 to 8 (inclusive) into 5 points, dividing the space between each part linearly.
print(zeroToEightEven) # '[0. 2. 4. 6. 8.]'

# Creating an array of random values of type 8-bit integer
shortInts = np.empty(3, dtype=np.int8)
```

## Matrices and Operations
So far, this page has only discussed one-dimensional arrays, which only represents a small part of what NumPy has to offer. In this section two-dimensional arrays (matrices) will be discussed, however arrays can be created in even higher dimensions in the same way.

The matrices in NumPy act like matrices seen in algebra courses, which means that they store a two-dimensional grid of values. A matrix with 3 rows and 5 columns has shape represented by the tuple (3, 5), and an array with 5 elements has shape (5, ). There is only one shape attribute in the array's tuple due to it having only one dimension.

Similar to how arrays are created, matrices can be created using a two-dimensional Python list, however it is important to note the matries must have a constant number of elements in each row (inner list), following in the same logic that an algebraic matrix cannot have missing values in a given position on the grid. Below are some examples of how to properly and improperly create matrices, an example of a 3-dimensional array, as well as some basic operations that can be carried out with them:
```py
# This will create a basic matrix with 3 rows and 5 columns
matrix = np.array([[1, 2, 3, 4, 5], [6, 7, 8, 9, 10], [11, 12, 13, 14, 15]])

# Indexing works as expected, like Python lists
print(matrix[1][0]) # '6'
print(matrix[0]) # '[1 2 3 4 5]'
print(matrix)
"""
[[ 1  2  3  4  5]
 [ 6  7  8  9 10]
 [11 12 13 14 15]]
"""

# size returns total number of elements in the matrix
print(matrix.size) # '15'
# ndim returns number of dimensions
print(matrix.ndim) # '2'
# shape returns shape tuple
print(matrix.shape) # '(3, 5)'

# This matrix definition would raise an error, since each row has a non-fixed number of elements
# invalid = np.array([[1, 2, 3], [4, 5], [6]])

# Example of a three-dimensional array (3+ dimension arrays are commonly called 'tensors')
tensor = np.array([[[1, 2], [1, 2]], [[1, 2], [1, 2]]])
print(tensor)
"""
[[[1 2]
  [1 2]]

 [[1 2]
  [1 2]]]
"""

# shape will have three values since this object has three dimensions
print(tensor.shape) # '(2, 2, 2)'
```

Finally, it is important to be familiar with a few operations that can be performed on arrays. If you have taken mathematical classes which incorporate matrices in their coursework, you should be familiar with the concept of matrix addiion and scalar multiplication, which can both be performed using NumPy with operations referred to as aggregation and broadcasting, respectively.
Aggregation acts as the basic form of addition between arrays. You can aggregate two arrays of any dimension together if they match shape, but it is also possible to aggregate a matrix with another "matrix" with only one row, in which case that one row will be aggregated with each row in the other matrix. Addition with an array and a scalar value is also supported, in which case that one value will be added to each array element.
On the other hand, broadcasting acts as multiplication. You can broadcast an array with a scalar to multiply each element in the array by the scalar, or by an array of the same shape to multiply the two respective array elements in each position.
NumPy also provides a square() method which, as you may expect, returns an array of the same shape as the inputted one, but with each element squared; an average() method for calculating the average of an array, as well as a flip() method which returns the inputted array but with every element in reverse order. This reversal carries down all dimensions.
One final significant note to make is that since most of these operations return an array or a scalar, it is simple to chain these operations in order to represent more complex mathematical equations which involve a sequence of steps. Provided below is a block of code displaying how the functions described above work.
```py
# Definitions from earlier to be re-used:
"""
firstArray = np.array([4, 2, 3, 1, 5])
matrix = np.array([[1, 2, 3, 4, 5], [6, 7, 8, 9, 10], [11, 12, 13, 14, 15]])
"""
# Broadcasting with a scalar
print(firstArray * 0.5) # '[2.  1.  1.5 0.5 2.5]'
# Addition with a scalar
secondArray = firstArray + 1 
print(secondArray) # '[5 3 4 2 6]'
# Broadcasting with an array
print(firstArray * secondArray) # '[20  6 12  2 30]'
# NumPy square() method
print(np.square(firstArray)) # '[16  4  9  1 25]'

# Reversal of a matrix (reversal of rows as well as the elements within each row occurs)
matrixTwo = np.flip(matrix)
print(matrixTwo)
"""
[[15 14 13 12 11]
 [10  9  8  7  6]
 [ 5  4  3  2  1]]
"""
# Aggregation with matrix with only one row
print(matrix + firstArray)
"""
[[ 5  4  6  5 10]
 [10  9 11 10 15]
 [15 14 16 15 20]]
"""
# Aggregation with two matrices of equal shape
print(matrix + matrixTwo)
"""
[[16 16 16 16 16]
 [16 16 16 16 16]
 [16 16 16 16 16]]
"""
# Average of arrays of various shapes
print(np.average(firstArray)) # '3.0'
print(np.average(matrix)) # '8.0'
print(np.average(tensor)) # '1.5'
```

## Additional Resources

- [NumPy Home Page](https://numpy.org/)
- [Installing NumPy](https://numpy.org/install/)
- [NumPy Official Beginners Guide](https://numpy.org/doc/stable/user/absolute_beginners.html)
- [Video Tutorial for Beginners](https://www.youtube.com/watch?v=QUT1VHiLmmI&ab_channel=freeCodeCamp.org)
