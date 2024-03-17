# Behavioral Design Patterns

Behavioral design patterns in software engineering are a set of patterns that focus on the interaction between objects and how they communicate and collaborate with each other. These patterns address the assignment of responsibilities between objects, encapsulation of behavior, and the flow of control among them. They aim to improve the flexibility, extensibility, and maintainability of software systems by providing solutions to common communication and collaboration problems.

## Table of Contents

1. [Usefulness of Behavioral Design Patterns](#use)
2. Examples of Behavioral Design Patterns
    1. [Observer](#obs)
    2. [Strategy](#str)
    3. [Iterator](#itr)
    4. [Command](#com)
    5. Examples of other [Behavioral Design Patterns](https://refactoring.guru/design-patterns/behavioral-patterns)

## Usefulness <a name="use"></a>

Behavioral design patterns are useful when you need to define how objects interact in a flexible and reusable manner, ensuring that changes in one part of the system do not require modifications to other parts. They are particularly valuable in scenarios where the behavior of objects needs to vary dynamically during runtime. 

Now, we will dicuss some commonly used behavioral patterns with real world analogies to get some intuition about when these patterns can be useful and how they can be implemented. For UML diagrams and implementation details check out [Refactoring Guru: Behavioral Patterns](https://refactoring.guru/design-patterns/behavioral-patterns). 

## Observer Design Pattern <a name="obs"></a>

The Observer design pattern is a behavioral pattern where an object, known as the subject, maintains a list of its dependents, called observers, and notifies them of any changes in its state. This pattern establishes a one-to-many relationship between the subject and its observers, allowing multiple objects to react to state changes in the subject independently. Observers register with the subject to receive notifications and update themselves accordingly. The Observer pattern promotes loose coupling between objects, making it easier to maintain and extend systems by separating concerns and allowing objects to interact without having direct knowledge of each other. It's commonly used in event handling, user interface design, and other scenarios where objects need to be notified of changes in another object's state.

<p align="center">
<img width="676" align="center" alt="Screenshot 2024-03-17 at 8 58 15 AM" src="https://github.com/paridhi26/CSC311Project/assets/85652265/f554584c-b2aa-4838-99b8-6a15c46310c7"> 
</p>

Image from [Refactoring Guru](https://refactoring.guru/design-patterns/observer)

### Analogy

Let's consider a scenario of a news agency broadcasting news to its subscribers. Here's how the Observer pattern can be illustrated in this context:

1. **News Agency (Subject):** The news agency acts as the subject in this scenario. It broadcasts news updates to its subscribers.

2. **Subscribers (Observers):** These are the entities interested in receiving news updates. Each subscriber registers with the news agency to receive notifications whenever new news is available.

3. **News Update (State):** The news updates represent the state changes that trigger notifications. Whenever the news agency releases a new update, it notifies all its subscribers.

4. **Notification Mechanism:** The news agency maintains a list of subscribers and notifies them whenever a new update is available. Subscribers receive the notification and can then react accordingly, such as reading the news update or taking any relevant actions.

In this example, the Observer pattern enables the news agency to inform its subscribers about new news updates without them having to constantly check for updates. Subscribers can register and deregister as they wish, and the news agency can broadcast updates without needing to know the specific subscribers. This decoupling of the news agency and its subscribers promotes flexibility, scalability, and modularity in the system.

## Strategy Design Pattern <a name="str"></a>

The Strategy design pattern is a behavioral pattern that allows a class to define a family of algorithms, encapsulate each one as a separate object, and make them interchangeable. This pattern enables clients to choose a specific algorithm from the family of algorithms dynamically without modifying the client code. By encapsulating algorithms in separate classes and providing a common interface, the Strategy pattern promotes flexibility, modularity, and extensibility in software design. It's particularly useful when multiple algorithms exist for a task or when algorithms need to vary independently from the client that uses them.


## Iterator Design Pattern <a name="itr"></a>

The Iterator design pattern is a behavioral pattern that provides a way to access elements of an aggregate object sequentially without exposing its underlying representation. It allows clients to traverse the elements of a collection without needing to know its internal structure. The Iterator pattern typically consists of two main components: the Iterator interface or class, which defines methods for accessing elements sequentially, and the Aggregate interface or class, which defines a method for creating an iterator object. By decoupling the traversal algorithm from the collection, the Iterator pattern enhances the flexibility and reusability of both the collection and the traversal algorithm. It's commonly used in scenarios where collections vary in structure or where there's a need to iterate over elements in a uniform manner.


## Command Design Pattern <a name="com"></a>

The Command design pattern is a behavioral pattern that encapsulates a request as an object, thereby allowing for parameterization of clients with queues, requests, and operations. It separates the sender of a request from the receiver, allowing for decoupling and flexibility in how requests are processed. The pattern typically involves four main components: the Client, which creates and sets up commands; the Invoker, which executes commands; the Command, which defines an interface for executing operations; and the Receiver, which carries out the requested action. By encapsulating requests as objects, the Command pattern enables the implementation of operations such as undo functionality, remote execution, and logging, among others, in a reusable and extensible manner.



## Further Reading <a name="further-reading"></a>
[Refactoring Guru: Behavioral Patterns](https://refactoring.guru/design-patterns/behavioral-patterns)
