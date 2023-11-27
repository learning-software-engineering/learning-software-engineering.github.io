# Learning NumPy

## Table of Contents

### [Introduction](#introduction-1)

### [Set Up](#set-up-1)

### [Array Basics](#array-basics-1)

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
The most basic object to create in NumPy is the array, which is similar to the default Python list, however it is designed to be more efficient, flexible, and comes with a variety of additional methods. An array can be created with an inputted Python list:
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

## Additional Resources

- [NumPy Home Page](https://numpy.org/)
- [Installing NumPy](https://numpy.org/install/)
- [NumPy Official Beginners Guide](https://numpy.org/doc/stable/user/absolute_beginners.html)
- [Video Tutorial for Beginners](https://www.youtube.com/watch?v=QUT1VHiLmmI&ab_channel=freeCodeCamp.org)
