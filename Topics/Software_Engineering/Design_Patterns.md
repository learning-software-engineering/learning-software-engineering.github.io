## Design Patterns

### Introduction

A design pattern provides a general solution to common problems in software design. These solutions are merely blueprints and may need to be modified to solve your current problem.  [ Add more intro stuff here]

### Iterator 

**Problem:** Given a collection of items, we want to iterate over the items in different ways(in order, bread-first, etc.). Also, we want to hide the underlying representation of the collection.

**Solution:** Create an iterator interface. Each iterator algorithm becomes a class that inherits from the iterator interface and overrides the methods accordingly [?].

<img width="400" alt="Screenshot 2023-11-21 at 10 29 07 PM" src="https://github.com/learning-software-engineering/learning-software-engineering.github.io/assets/97854264/1365cbc5-95b4-4138-9705-7608065a61a1">

**Benefit:** With an iterator interface, the client does not need to know the underlying representation of the collection, as they can use the iterator inteface to do traversal work. Also, all traversals algorithims over the  collection  are organized and coupled with the collection. More iterators can be added to the collection by adding new subclasses that  inherit from the interface. 

### Factory Method

**Problem:**  An instantiated class may change over time. For example, suppose you had a package delivery application that was only delivering by trucks but later also you started delivering by boats and trains. In that case, you need a way to introduce new modes of transportation without breaking existing client code and develop a way to organize the all the nodes that could be introduced.

**Solution:**  Create a general interface  with functions that every new object must implement. Then,  implement a new subclass for each object that inherits from the interface and override the function accordingly. [elaborate - how is this differnt from iteratore method- they all seem like you just have an interface....]

<img width="400" alt="Screenshot 2023-11-21 at 11 23 27 PM" src="https://github.com/learning-software-engineering/learning-software-engineering.github.io/assets/97854264/efb95d64-6ca0-44c6-8c1c-041125d27259">

**Benefit:**  A general interface standardizes the architectural model, allowing applications to develop their domain object and as many as needed. Also the client can use the methods in the abstract class (general interface) without knowing how the subclasses are implemented(?).

Maybe one more design pattern and elaborate more on the solution of these design patterns...

