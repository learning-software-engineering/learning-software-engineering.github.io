C++ can be a confusing language. Pointers, ownership, memory management -- there is a lot going on in even a simple C++ program and it is often difficult for beginners to approach. As students entering the workforce we want to learn how to write industry grade C++ that would impress our interviewers, coworkers, and employers. This guide gives an introduction to doing just this, covering some of the most important topics in object-oriented design in C++.

### So what is OOP?
Object-oriented programming or OOP are the fundamental principles that most modern languages are optimized to follow. We can summarize OOP with 4 primary concepts.
* **Encapsulation** is the principle of bundling data and the methods that operate on that data under a common slass. This allows us to hide the internal details of an object and restrict access to its state.
* **Inheritance** is the mechanism that allows a class to inherit the properties and behaviors of another, known as the parent class. This promotes code reusability and facilitates the creation of a hierarchical structure for classes.
* **Polymorphism** means "many forms" and is concept that allows objects of different classes to be treated as objects of a common parent class, enabling code to work with objects of various types in a uniform way. In particular, mechanisms like method overloading, defining multiple methods with the same name but different parameters, and method overriding, providing a specific implementation of a parent classes' method in a child class, make polymorphism possible.
* **Abstraction** involves simplifying complex systems by modeling classes based on the essential properties and behaviors that they share, focusing on what an object does rather than how it does it. This make it easy for code to be utilized by different developers and reduces complexity by hiding unnecessary details.

### Why is C++ a great language for upholding OOP principles?
C++ has a variety of features that make object-oriented design easy. For example, it supports the creation of classes and objects, the fundamental building blocks of OOP, allowing users to define classes to encapsulate data and methods and then create instances(objects) of those classes. Furthermore, access specifiers like public, private, protected allow programmers to control the visibility of class members further enforcing the principle of encapsulation. C++ also supports both single and multiple inheritance, allowing classes to inherity properties and behaviors from one or more parent classes, giving us flexibility in our class hierarchies. Additionally, C++ has both compile-time (method overloading) and runtime polymorphism (method overriding); these tools not only enable polymorphism but also abstraction as they allow us to define abstract classes, facilitating the implementation of abstraction.

We are going to explore OOP by tackling an object-oriented design problem, but before that we should talk about some important concepts and tools that make C++ special as well as the best practices that Google recommends for using them.

#### Header Files
In C++, header files (.h) are used to provide an interface to other parts of the program. Think of it as the bridge that connects .cpp or .cc files (the files containing our C++ source code). In them, we declare the structure and characteristics of entities without defining how they are implemented. Usually, we want to have one header file per source file. 

While not enforced semantically, header files should ONLY include what you use. If your source file has a helper function foobar() that will only be called within the source file, don't include it in your header file! This goes both ways. If your source file isn't using at least one of the declarations within a header file, don't include that header file! Additional #include statements force the compiler to open more files and process more input, slowing down compile time.

Moreover, ALL header files should begin with the #define guard. For big projects, it can be easy to lose track of where a file has already been included. These guards help prevent circular dependencies by restricting the inclusion of a file if it has already been defined.
```
#ifndef FOO_BAR_BAZ_H
#define FOO_BAR_BAZ_H
...
#endif
```

#### Structs in C++
If you have learned C, you may be familiar with the concept of structs. C++ also has structs, however, in addition to that, we also have classes. Although the two keywords behave basically the same in C++, we should ONLY use a struct for passive objects that carry data. Everything else should be a class. All fields of a struct should be public and as a result, should not have rules that imply relationships between different members, since direct access can break those rules.

As Google says, when in doubt, make a class.

Nevertheless, when elements can have meaningful names (but not require some high level of functionality that would suit a class), we should prioritize a struct over pairs and tuples.

#### Operator Overloading
You can redefine what certain operators mean in C++. However, don't go crazy and make + actually perform *. An operator should only be overloaded when their meaning is obvious and consistent with built-in operators. For example, using + to concatenate two strings.

#### Ownership
This is a big topic that can get quite complex, but in the end it really boils down to one question: who should own this object? For example, when creating a banking system it makes sense that the Bank should own all instances of Account. Don't make the bank store references to the Account, this makes it confusing when handling the dynamic memory associated with the object. The Bank's scope should control the existence of the Account in memory. If the Bank disappears simultaneously the Account disappears (and your money!). Additionally, the Account should only be erasable through the Bank. Imagine if the contract your signed owns your Account and ripping that contract simultaneously deletes your Account (and your money!), yikes.

To handle ownership, modern C++ has this fancy mechanism called smart pointers. Smart pointers automatically handle memory allocation and deallocation. The only decision you need to make is who owns the smart pointer (in our prior example of Bank and Account, the Bank should own the smart pointer to Account). More on smart pointers below.

#### Smart Pointers
There are a few types of smart pointers: unique_ptr, shared_ptr, and weak_ptr. I will leave it up to you to learn the differences. Below are some basic guidelines that will (hopefully) help you utilize smart pointers effectively and correctly, preventing memory leaks and/or loose pointers.

* NEVER use new or delete. This makes it unclear whether a pointer owns the object or doesn't.
* Use unique_ptr by default because it has basically no overhead. If you know for sure that there will be several owners, use shared_ptr.
* When a pointer will not own the object, use raw pointers. For example, passing an object to a function should be done using a raw pointer. Going back to our example, it never makes sense to transfer ownership of an Account to anything other than the Bank. To pass a unique_ptr as a raw pointer to a function, the best way is to dereference it and pass it by reference using .get().
* Do NOT use delete on a raw pointer, assume that you have followed the previous steps correctly in which case a raw pointer should never own the object.
* When you create an object and want to return it, return it as a smart pointer. This will transfer the ownership of that object to whatever is receiving the function's return value. If you don'tdo this, you're probably going to get a memory leak.
* When you need to transfer the ownership of a smart pointer. Use std::move(). This basically does the same thing as the previous point.

If you can manage your memory well. C++ will be a piece of cake.

### Example
Now let's consider the following object-oriented design problem.
