## Code Smells

### What is code smell?

Code smells are indicators of potential issues or weaknesses in software code. They are not bugs or errors, but rather patterns or 

practices that may lead to problems in the future. 

# Common Types of Code Smells and How They Can Harm your Code

There are a vast number of code smells and they differ from project to project and developer to developer, and business to business. 

So, it is crucial to thoroughly understand the organization’s design and development standards before handling any code smell. 

Here are the most common code smells that developers usually encounter with:

## Duplicate Code

In simple terms, duplicate code happens when two code fragments look almost identical. Consider this piece of code:

```
def calculate_rectangle_area(length, width):
    return length * width

# Duplicate code
def calculate_square_area(side):
    return side * side
```

In this example, the calculate_square_area function duplicates the functionality of the calculate_rectangle_area function but only for squares. This coding habit

makes it harder to debug a program because any changes or bug fixes need to be applied to multiple places. Also, duplicated code makes the codebase harder to read 

and understand. Developers might need to analyze multiple sections of code that are essentially doing the same thing.

## Improper Names

If your variables, classes, and functions lack proper names, this can be an indicator that your code isn’t clean. For example, 

```
def func(a, b):
    return a + b
```
This function is simple enough to understand despite its naming issue. However, imagine that we have a big function to perform some backend tasks for our program,

then it would be more problematic for other developers.  Without additional context or comments, it's not immediately clear what the function is supposed to do. 

This can lead to confusion for others who encounter this code later or who need to work with it.

## Dead Code 

## Middle Man

## Feature Envy

## Long Functions

## Data Clumps

## Comments


