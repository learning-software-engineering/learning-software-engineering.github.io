## Code Smells
Code smells refer to certain types of code that, while functional, will require increasing accommodation as more code begins to rely on the "smelly" code. While it is possible to ignore these types of code,
the longer that they remain, the harder it becomes to fix issues they directly or indirectly cause in the future. Therefore, it's in a developer's best interest to be familiar with a broad spectrum of code smells
so that they may identify and eliminate them as soon as possible.


## A Motivating Example
Consider the following snippet of code:

```
class Something:
     temp_field: int
     
     def do_something(self) -> int:
         if self.temp_field == None:
             return -1
         else:
             return self.temp_field + 1
```
On its own, this code is functional, but it raises a number of questions. For example: when exactly is `temp_field` equal to `None`? When does it actually store relevant data? This answer is
largely dependant on how the class `Something` is used, but the specifics may not be clear to someone reading this code. 

This code smell is known as a "Temporary Field", which is when classes are given attributes to be used in some of their methods, but in some cases the attribute stores null values. While adding null checks
easily allows code using these attributes to function, it decreases code readability, and if the technique is abused it can easily lead to unnecessarily long code. To fix this, refactoring is required.

## Refactoring


## Categories


## More Info
