# Creational Design Patterns

## What are they?

As the name suggests, creational design patterns deal with the creation and maintenance of objects in object-oriented programming. They are used to instantiate different classes of objects and their subclasses in the best way to achieve their intended purposes.

There are 5 major types of creational patterns that are commonly used in software development.

## Types of Creational Design Patterns

### Simple Factory

#### Usage

A complex object needs to be created multiple times.

The simple factory works by delegating the instantiation of an object class to a dedicated method. This allows the object to be hidden from the user endpoint, by preventing the need to directly instantiate (and thus access) the object.

#### Structure

A factory class is introduced in addition to the object class. The factory has a create method, whose purpose is to generate and return an instance of the object class.

<p align="center">
<img width="690" alt="UML of Simple Factory design pattern" src="./System_Design/assets/Simple Factory.png">
</p>

#### Benefits

- Hides the object class creation behind a layer of abstraction. Can be used to simplify the object creation provided a few parts need to be built before instantiation, or adjustments need to be made after instantiation.

### Factory Method

#### Usage

A singular class of objects needs to be produced multiple times, and in a dynamic way via subclasses of the object.

The factory method design pattern introduces a class containing a singular create method that creates one class of objects (products). Extensions of the factory class are created as needed to override the default implementation (or abstraction) of the create method to produce different subclasses of the product.

#### Structure

A factory class containing one (abstract) create method that produces a product class of the required type. Implementations of the factory override the create method as required to output subclasses of the product.

<p align="center">
<img width="690" alt="UML of Factory Method design pattern" src="./System_Design/assets/Factory Method.png">
</p>

#### Benefits

- Allows variations of the product class to be easily created without having to define new calling behaviour in programs utilising the product and factory classes.

### Abstract Factory

#### Usage

when there are multiple related object classes that need to be separately instantiated using different creation processes.

An abstract factory is a factory of factories: it is a design pattern that takes advantage of abstraction and inheritance to define a common public API for factories of a set of related subclasses of some parent class. This allows the user of the factory to define functions and creation behaviour for an extendible set of classes, each of which can have a different object construction process under the hood, without having to define if-else behaviour for every single subclass factory in dependent methods. As with all abstract classes, this allows extension and modularity as a result of not relying on the internal workings of specific factory classes relating to certain subclasses.

Note that this differs from the factory method in that a singular abstract class is introduced to deal with the creation of _multiple_ related products.

#### Structure

An abstract factory class contains multiple factory methods, each producing a different, but related, abstract class of objects. Implementations of the abstract factory implement these methods to produce (different) subclasses of the abstract object classes.

<p align="center">
<img width="690" alt="UML of Abstract Factory design pattern" src="./System_Design/assets/AbstractFactory.png">
</p>

#### Benefits

- By using an abstract factory, the user is able to avoid having to implement separate code for each different object factory necessary for their product.
- As with the factory method, the object creation system becomes highly extensible: if a new extension of an object is declared, the user can simply create another implementation of the abstract factory to produce it, without having to change the behavior of any other classes/functions that utilise the factory.

### Singleton

#### Usage

A class or resource needs to only have one central instance that is globally accessed across the program.

A singleton achieves 2 purposes: it maintains exactly 1 instance of a given class  across the entire program, and it provides a global access point to that class. It achieves this by first hiding the default constructor of the original class, and then providing a static constructor for the class. The first time the constructor is called, it generates an instance of the class and caches it within a static variable. Further calls to the constructor return the cached instance rather than creating a new one.

Note that this differs from the factory method in that a singular abstract class is introduced to deal with the creation of _multiple_ related products.

#### Structure

The simplest implementation of a singleton design pattern consists of the desired class, adjusted to contain an instance of itself, the default constructor hidden and a getInstance method that returns the cached instance if not null, and creates a new instance(storing in the cache) if the cache is null. If the original object should not be modified, the singleton class can store it in its static cache, and should be used to get instances of the object using the getInstance method call, rather than making direct instances of the object.

<p align="center">
<img width="690" alt="UML of 2 different Singleton design patterns" src="./System_Design/assets/Singleton.png">
</p>

#### Benefits

- Maintain and access a central resource with a singular call to the singleton.

### Builder

#### Usage

A highly complicated and modular object needs to be created in a step-by-step process, multiple times. Some steps may differ between iterations.

A builder is a design pattern that is deployed to automate the instantiation of objects that require a step-by-step process to deal with many nested parts. It works by splitting the creation of each nested part/step into a separate method within the builder class. A director class is also introduced in order to handle the ordering/calling of these steps for a chosen builder class. By taking advantage of instantiation, it is possible to extend a given builder class or director class and override one or more methods to partially alter the creation process without having to redo the entire creation process.

#### Structure

The builder design pattern typically consists of an abstract builder class containing the methods(steps) common to all building processes for the given family of products, concrete implementations of that class that override/implement methods of the abstract builder, and a director class that stores a builder object and controls the calling of methods for the process.

<p align="center">
<img width="690" alt="UML of Builder design pattern" src="./System_Design/assets/Builder.png">
</p>

#### Benefits

- Simplifies the creation process of complicated objects.
- Allows the adjustment of individual steps without having to rewrite the entire creation process.

## Further Reading <a name="further-reading"></a>

Refactoring Guru provides a detailed reference guide with examples for creational design patterns, as well as other design patterns that can be useful to implement in the right scenarios.

[Refactoring Guru: Creational Patterns](https://refactoring.guru/design-patterns/creational-patterns)

Source Making also provides a more technical description of the same: it can be useful to understand the structure of these design patterns.

[Source Making: Creational Patterns](https://sourcemaking.com/design_patterns/creational_patterns)

