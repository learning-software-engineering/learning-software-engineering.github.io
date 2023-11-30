# Test Driven Development 101

## Table of Contents:
### [What is Test Driven Development (TDD)](#introduction)
### [TDD Development Cycle](#tdd-development-cycle)
### [Pro's and Cons](#pros-and-cons)
### [Type's of Testing](#types-of-testing)
### [Conclusion](#conclusion)



## Introduction

Test Driven Development (TDD) is a development practice in which developers create a set of tests before implementing the code that they are going to test. The idea is that the developer writes tests around the expected results and requirements which they know in advance.If the tests pass after implementing the software then the developer can have confidence that their code is working as expected. On the other hand if any of the tests fails then it signals to the developer that something is wrong.


## TDD Development Cycle

A common phrase you might see when talking about TDD is the "Red-Green-Refactor" cycle. This cycle is the key principal in TDD. This cycle refers to the three states that occur when developing using this practice.

**Red State**: When the developer initially writes tests that are going to fail because they are simply not implemented yet or there have been changes in the requirements

**Green State**: When the developer writes code so that all the tests pass which ensures that the requirements and expected behaviours are met

**Refactor State**: Once the tests have passed you can go back and clean up the previously written code in any which way you want, so that there is less duplication or readability etc.

The core concept behind TDD is that once you get to the refactor state you should have already had a working version of your code, so if in the process of refactoring you change a behaviour the tests will once again return back to the red state and the cycle continues.

#### Example

For example lets say we want to make a calculator program in python, and we know want that calculator to have a multiplication function. This is how that might look if we are using TDD

This example will be written in python and uses the doctest package for tests

First we will create our class with some examples that will tests if our implementation is correct 

 ```python:
import doctest

class Calculator:
    """
    A simple calculator class that can multiply.

    Examples:
    >>> calc = Calculator()
    >>> calc.multiply(2, 3)
    6
    """

if __name__ == "__main__":
    doctest.testmod()
 ```

This code will fail because we haven't implemented the multiply method yet but it showcases how we expect the method to behave. This is our **Red State**

We then move on to implementing the methods and update our file like so
 ```python:
import doctest

class Calculator:
    """
    A simple calculator class that can multiply.

    Examples:
    >>> calc = Calculator()
    >>> calc.multiply(2, 3)
    6
    """

    def multiply(self, a, b):
        product = 0
        for i in range(0, b):
            product += a
        return product

if __name__ == "__main__":
    doctest.testmod()
 ```

 At this point the test we wrote is now passing so we know that the method we just implemented is working the way we intended it to work. This is our **Green State**

 Now that we have a Green state we can move on to our **Refactor State**. If we change our multiply method fundamentally and alter its behaviour our original test will once again fail indicating that our refactor changed the behaviour, we want to refactor without changing any behaviour. We update our file like so.

  ```python:
import doctest

class Calculator:
    """
    A simple calculator class that can multiply.

    Examples:
    >>> calc = Calculator()
    >>> calc.multiply(2, 3)
    6
    """

    def multiply(self, a, b):
        return a * b

if __name__ == "__main__":
    doctest.testmod()
 ```

Our tests are still passing which means our refactor did not change any behaviour while we were able to optimize the code.

This is a trivial example of TDD and following this pattern if we wanted to add more methods like add and subtract we can follow similar steps and be confident that those changes don't effect multiply as long as the multiply test is still passing

## Pros and Cons

You might be thinking to yourself "wow TDD seems great, it ensures that the code does exactly what you want it to do why is this not the standard?". For as great as a principle TDD is it also has its drawbacks, its up the developer to decide whether or not TDD fits their use case.

#### Pros
- **Easy Detection of Bugs**: Since you write tests early into the development process you are able to catch bugs earlier on
- **Code Quality**: Usually as a by product of TDD the developer has to think a little more about the design of the code leading to better code quality overall
- **Regression Testing**: All the tests that are written provide a thorough test suite which can be run (usually using CI) to ensure that any changes haven't broken other parts
- **Documentation**: The tests are self documentation of the code as they should show how to use the code and the behaviour of the code

#### Cons
- **Time-consuming**: Writing comprehensive tests for your code before you start actually coding takes a lot of time, especially the initial cost of creating something new
- **Maintenance of Test Suite**: As the code base grows larger that means the tests need to be updated accordingly. Staying on top of this once again has a large time cost
- **Over Testing**: While having tests are a good thing sometimes the focus might shift too much to the tests where there are simply too many tests or that the code is written simply to pass a test
- **Learning Curve**: Typically writing tests include using a library or framework of some sort to do the testing. This means that the developer has to learn how to use this framework in addition to the environment which they are developing

## Types of Testing

Typically for TDD the type of tests written are unit tests, where we test a singular unit (i.e function,method,class). This way we can have confidence that the individual smaller parts of our entire system are working and if all the small parts work individually we either have a working system or an easier time debugging which area of the system is misbehaving. Unit tests are usually the go to when it comes to TDD.

End-to-end(E2E) tests are more concerned about how different parts of the entire system are connected. They test the cohesion of all parts of the system whether that includes the frontend,backend,database etc. They typically test how users will interact with the system and ensure that services are running correctly. E2E tests are more related to behaviour driven development(BDD) which is out of the scope of this article but there will be links at the bottom to learn more.

## Conclusion

Test driven development is a methodology where you first write tests outlining how you want the code to work and then write the code to achieve that behaviour. The idea behind this concept is that there is an initial investment of time and complexity but it forces the developer to write better code that will be easier to maintain in the future and that the time saved in debugging and maintenance will offset the initial investment. However TDD is not a one-size-fits all and there are scenarios in which TDD can have more downsides than rewards.

#### Extra Resources

Videos: 
[Jim Coplien and Bob Martin Debate TDD](https://www.youtube.com/watch?v=KtHQGs3zFAM)
[YOU DONT UNIT TEST???](https://www.youtube.com/watch?v=pvBHyip4peo)
[Test-Driven Development // Fun TDD Introduction with JavaScript
](https://www.youtube.com/watch?v=Jv2uxzhPFl4)

Articles:
[What is Test Driven Development](https://www.guru99.com/test-driven-development.html)
[Test-driven development - IBM Garage Methodology](https://www.ibm.com/garage/method/practices/code/practice_test_driven_development/)

Popular Testing Frameworks:
[Cypress](https://docs.cypress.io/guides/overview/why-cypress)
[PyUnit](https://wiki.python.org/moin/PyUnit)
[doctests](https://docs.python.org/3/library/doctest.html)
[JUnit](https://junit.org/junit5/)
[Jest](https://jestjs.io/)

BDD:
[What is BDD? - Agile Alliance](https://www.agilealliance.org/glossary/bdd/)
[What is BDD? - Browser Stack](https://www.browserstack.com/guide/what-is-bdd)
[TDD vs BDD](https://www.youtube.com/watch?v=Bq_oz7nCNUA)