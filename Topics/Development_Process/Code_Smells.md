## Code Smells
Code smells refer to certain types of code that, while functional, will require increasing accommodation as more code begins to rely on the "smelly" code. While it is possible to ignore these types of code,
the longer that they remain, the harder it becomes to fix issues they directly or indirectly cause in the future. Therefore, it's in a developer's best interest to be familiar with a broad spectrum of code smells
so that they may identify and eliminate them as soon as possible.


## A Motivating Example
Consider the following snippet of code:

```
class Something:
     temp_field: int
     
     def do_something(self) -> int | None:
         if self.temp_field == None:
             return None
         else:
             return self.temp_field + 1
```
On its own, this code is functional, but it raises a number of questions. For example: when exactly is `temp_field` equal to `None`? When does it actually store relevant data? This answer is
largely dependant on how the class `Something` is used, but the specifics may not be clear to someone reading this code. 

This code smell is known as a "Temporary Field", which is when classes are given attributes to be used in some of their methods, but in some cases the attribute stores null values. While adding null checks
easily allows code using these attributes to function, it decreases code readability, and if the technique is abused it can easily lead to unnecessarily long code. To fix this, refactoring is required.

## Refactoring
Refactoring is a software development practice in which code is rewritten such that no new functionality is actually provided, but the code becomes cleaner and better accommodates future extensions of 
features. While it is generally recommended in software development that code should not be rewritten, but extended (see the [Open/Closed Principle of SOLID](../Development_Process.md#solid-principles), refactoring typically prevents more significant amounts of code rewriting that may be required in the future.

Many refactoring solutions to code smells are well-established and should be drawn upon once relevant code smells are identified. One such solution for the previous example is known as "Introduce Null Object", in which
attributes that may be null should be defined over a new "Null" class, which can provide default values when the aforementioned attribute would have previously been null. This contains any null checks to the new class,
allowing for the removal of if-statements in other code that may cause confusion or excessive code length. Furthermore, future code that may deal with the previously temporary field will also no longer need
any null checks, as the new class does it for them. Thus, refactoring improved both the readability and extendability of the former code.

## Categories
While there may be many different types of code smells, all of them fall into one of five categories which can more easily be identified when writing code. The categories are as follows:
- Bloaters
- Object-Oriented Abusers
- Change Preventers
- Dispensables
- Couplers

## More Info
