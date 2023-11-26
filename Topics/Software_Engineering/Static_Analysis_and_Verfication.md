# Introduction to Static Analysis and Formal Verification

## Table of Contents:
- ### [Example Applications](#Example-Applications)
- ### [Static Analysis](#Static-Analysis)
- ### [Formal Verification](#Formal-Verification)
- ### [Additional Resources](#Additional-Resources)
___



## Example Applications

People write software for a variety of purposes, ranging from simple e-commerce websites to helping navigate space rockets.
In the former example, the risks are small. A bug in the code might mean a product might not be rendered properly, or trying to access a page returns an error.
In the latter example, the risks are huge. A bug in the code could cost millions of dollars or even the lives of real people.

This has happened, most notably to the Ariane 5G rocket in 1996, where an integer overflow error led to the rocket veering off course and self-destructing. 

High risk applications are not limited to just space travel. Various forms of transportation including cars, healthcare, security, nuclear energy, and plenty more high-risk industries depend on software.

Thus, as a developers, we should be equipped with the tools to not just be confident in our code, but to test it in a way that is rigorous and ensures no errors are present. 

It should be noted that the following sections are not comprehensive, as these are large theory heavy fields, which a thorough understanding of will require extensive research and learning. 

## Static Analysis

In large software systems, it can be infeasible to write a test case for every single possible scenario in the code.

Static analysis is the practice of analyzing and reasoning about programs without executing them.

Static Analysis can be performed by both humans, and automatically using various tools to help us better understand our code. 

It should be noted, that these methods cannot be completely relied upon, as it's impossible to find every error for an arbitrary program, as the task reduces to the [halting problem](https://en.wikipedia.org/wiki/Halting_problem).  

You have almost likely used static analysis tools before, even if you haven't realised it, as most modern IDE's implement some form of it.

### Dataflow Analysis

- Technique for gathering information about the possible data available at any point in the program.
- Examples include 
  - Live Variables Analysis: Keeping track of which variables might be read again before they are written to. (Helps with memory management by freeing values which won't be accessed)
  - Available Expressions Analysis: Keeping track of which expressions have already been calculated at a program point. (Helps with debugging, your IDE can tell you that you're accessing a variable that might not be initialized)
- As a developer, you'll likely never need to go out of your way to use dataflow analysis, but it's valuable to be aware of it and understand it.

### Linters

- A more general form of static code analyzers.
- Usually includes some form of dataflow analysis, in addition to syntax checking, pointing out dangerous use of language features such as goto statements.
- Often always includes style checking and suggestions, as a means to keep code style consistent and readable. 
- Most Major IDE's implement a linter, as thus you'll likely never need to go out of your way to use one. However, for a single language there are commonly a few different common linters which may suit certain developers preferences.

## Formal Verification

A rigorous process to ensure "correctness" of software by mathematically proving the satisfaction of a given specification

It is generally considered the highest level of assurance in software, and requires a developer knowledgeable about the code they are trying to verify, even though there are tools available.


### Model Checking

- Method for reducing a model to a graph of finite-states, and checking that each state meets a given specification. 
- We can check that these states satisfy requirements such as not representing a crash. 
- We define requirements as propositional logic formulas, and states as structures to satisfy them.
- Generally model checkers work by defining these states, or groups of states symbolically, and exploring every state to check if it satisfies the specification. 
- Examples Include
  - [SPIN](https://spinroot.com/spin/whatispin.html): A full [Linear Temporal Logic](https://en.wikipedia.org/wiki/Linear_temporal_logic) model checking system, mostly used for the verification of multithreaded or distributed software. 
  - [NuSMV](https://nusmv.fbk.eu/): A symbolic model checker used for checking embedded systems against given constraints. 
- In general, tools are very specific to a language and task, and most practical use cases are in hardware, software which interacts with hardware, or very low level coding tasks. 
- Understanding the model checking from a theoretical standpoint is a difficult task, and as a developer, only something you should invest in if you know it'll be worthwhile for you. 


### Deductive Verification

- Similar to what you may have done in CSC236, it consists of formally defining specifications and proving that a piece of code fits it.
- Generally implemented as Automated Theorem Provers, which can be used to check and help verify programs, often including to ability to provide counterexamples to incorrect programs.
- Examples Include
  - [Z3](https://microsoft.github.io/z3guide/docs/logic/intro/): An SMT solver: Takes in sequence of theorems that define a model, and decides is they are "satisfiable" (There exists a solution).
  - [Isabelle](https://isabelle.in.tum.de/): Allows proofs to be written in procedural or declarative styles, and verifies is the proof is valid. It was notably used to verify the C programming language.
  - [Dafny](https://dafny.org/): A usually educational tool, that allows you to write programs which compile to other languages such as Python, and write verifiable proofs using assertions, invariants and lemmas. 
- Most tools are reasonable easy to learn for a developer with a background in mathematical proofs, especially relating to program correctness. Thus, learning to use Theorem Provers can be valuable for an average developer looking to get into applications where correctness is crucial. 

## Additional Resources

- [The Calculus of Computation](https://link.springer.com/book/10.1007/978-3-540-74113-8)
- [Static Program Analysis](https://cs.au.dk/~amoeller/spa/spa.pdf)
- [CSC410](https://artsci.calendar.utoronto.ca/course/csc410h1)