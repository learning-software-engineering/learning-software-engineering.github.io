## Design Patterns

### Introduction

A design pattern provides a general solution to common problems in software design. These solutions are merely blueprints and may need to be modified to solve your current problem.  [ Add more intro stuff here]

### Iterator Design Pattern

**Problem:** Given a collection of items, we want to iterate over the items in different ways(in order, bread-first, etc.). Also, we want to hide the underlying representation of the collection.

**Solution:** Create an iterator interface. Each iterator algorithm becomes a class that inherits from the iterator interface.

<img width="200" alt="Screenshot 2023-11-21 at 10 29 07 PM" src="https://github.com/learning-software-engineering/learning-software-engineering.github.io/assets/97854264/1365cbc5-95b4-4138-9705-7608065a61a1">

**Benefit:** With an iterator interface, the client does not need to know the underlying representation of the collection, as they can use the iterator face to do traversal work. Also, all traversals over the same collection are coupled with the collection and are in one space. More iterators can be added to the collection by having them inherit the interface. 
