# Design Patterns for Beginners

## Introduction
Design patterns are solutions to common problems encountered in software design. They provide a 'systematic' yet creative way to design and solve problems. When you're building software, you often face similar challenges, and design patterns offer a way to address these challenges in an efficient manner.

### Why Design Patterns?

1. **Reusability:** Design patterns promote code reusability. Once you understand and implement a design pattern, you can apply it to different projects and scenarios. Note that it is not a piece of code for you to copy and paste, but a certain way of thinking and solving problems. 
   - But it is not the same as _algorithm_, whose input and output satisfy a certain specifications. Design Patterns are more creative and applicable in software development, in the sense that it does not require a strict specification on its input. Although both of them can be applied to any programming languages, their distinction cannot be ignored.  

2. **Maintainability:** Using design patterns results in cleaner and more maintainable code. They encapsulate specific behaviors, making it easier to modify or extend functionalities without affecting the entire codebase.

3. **Scalability:** Design patterns contribute to scalable and flexible software architecture. They help in building systems that can adapt to changing requirements and scale gracefully.


## Types of Design Patterns
In this short introduction, we will use an Objected Oriented Programming (OOP) language as the underlying programming languages. Please be aware of the relationship between OOP and Design Patterns. Design Patterns are more general and can be applied to any programming languages, not just OOP ones; but good OOP principles usually adhere to design patterns closely. 

### 1. Creational Patterns
Creational patterns focus on object creation mechanisms, dealing with the process of object instantiation.

### 2. Structural Patterns
Structural patterns are concerned with object composition, forming relationships between objects to create larger structures.

### 3. Behavioral Patterns
Behavioral patterns define ways for objects to communicate, encapsulating patterns of communication between objects.

## Simple yet Powerful Example
We briefly introduce a **Creational Pattern** to demonstrate how powerful and flexible design patterns are. 

Suppose we are developing a software where transportation tools are involved. At first, we only support cars and busses. But as our product grows, we have the need to support more types of transportation tools, like airplanes and boats, etc. We can certainly create more classes, like we did for cars and busses. 

But sometimes all we care about is that they are methods of transportation, i.e., they can take people from one place to another place. Let's call that behavior `move`. So if `x` is an object of class `car`, it can move like this: `x.move()`. 

So instead of creating more classes of transportation tools, we can define a more general class called `Vehicle`, each of whose object must have a behavior named `move`. So we may consider `car` and `airplane` as a `Vehicle` object! Even better, from now on, no matter what class we intend to create, as long as it has a behavior of `move`, we may treat it as an object of `Vehicle`! So that whenever we want to have some other functionalities involving `move`, we can simply treat them as `Vehicle` objects, instead of changing the behavior of those classes repeatedly. 

To give an example in Python:

The following code snippet creates a class called `Vehicle` in Python:
```python
class Vehicle:
    def move(self):
        raise NotImplementedError
```

In order to treat every instance of `Airplane` and `Car` as a `Vehicle` object, we might write:
```python
class Airplane(Vehicle):
    def move(self):
        # Actual code to make Airplanes move
```
and 
```python
class Car(Vehicle):
    def move(self):
        # Actual code to make Airplanes move
```


This way, we don't need to worry about the exact details of 'how a car/plane' moves, but knowing that they support `move()` is good enough. 


## Helpful resources
### Online Courses:
- **Coursera - "Design Patterns" by the University of Alberta:**
   - This online course covers design patterns using Java. It includes video lectures, quizzes, and programming assignments to reinforce the concepts.

### Websites and Tutorials:

-  **[Refactoring Guru - Design Patterns](https://refactoring.guru/design-patterns):**
   - This website provides a comprehensive guide to design patterns with examples in multiple programming languages. **EXTREMELY RECOMMENDED!**


- **[DZone - Design Patterns Refcard](https://dzone.com/refcardz/design-patterns):**
   - DZone offers a concise reference card on design patterns, providing a quick overview of essential patterns.

### Online Communities:

-  **[Stack Overflow - Design Patterns Questions](https://stackoverflow.com/questions/tagged/design-patterns):**
   - Stack Overflow is an excellent place to find answers to specific design pattern-related questions and engage with the programming community.

