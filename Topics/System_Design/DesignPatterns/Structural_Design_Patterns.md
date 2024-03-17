# Structural Design Patterns

**Structural Design Patterns** are an important category of design patterns that help software enginners to create well designed, flexible and structured bif software prjects. To be more precise, structural design patterns are about assembling, combining, and composing objects and classes into larger structures, while still making sure these structures are flexible and efficient. They simplify the design of big software project by allowing us to identify relationships between entities (classes or interfaces). 

In this tutorial, we will go through several important design patterns that belong to the category of Structural Design Patterns.

## *Adapter Design Pattern*
### Goal and What It Does: 
Let's suppose that there is a client code which has a target class regarding its domain. Consider that there is another class that has an interface that is not appropriate to be combined and matched with the interface of the client class. The **Adapter  Design Pattern** adjusts the interface of the class (which has the  inappropriate and incompatible interface) into another interface that is compatible with the client code and domain.  It wraps an existing class that is incompatible with a new interface that allows it to be compatible with the client code.  In other words,  Adapter allows classes that are not compatible currently, to work together and be assembled together. 

### Example Scenario:
Let's give a small real-world example (scenario) where the Adapter Design Pattern is useful. Suppose that in a company working with optical instruments, all the functionalities regarding the manipulations of the resulting data received from an instrument as well as those for the data that users send to the instrument are done in MATLAB programming language. However, consider there is a functionality that is written in C# programming language related to communicating with the instrument.  We can change the code written in C#  to be written in MATLAB but this might cause issues because communication with the instrument works well in C#. 