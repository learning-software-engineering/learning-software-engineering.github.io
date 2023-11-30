## Resources for Development Process

## Git

### [Learning Git](./Development_Process/Git/Git.md)

### [Trunk-Based Development](./Development_Process/Trunk_Development.md)

### [Django Project Deployment: AWS, Vercel, and Railway](./Development_Process/Django_Deployment_AWS_Railway_Vercel.md)

### [Node.js Project Deployment: Azure](./Development_Process/Azure_webapp_deployment_with_nodejs.md)

### [Automated Frontend Deployment with Vercel](./Development_Process/Frontend_Automated_Deployment_Vercel.md)

### [Flask Application Deployment on Heroku](./Development_Process/Flask_App_Deployment_Heroku.md)

### [Quality Assurance Testing](./Development_Process/QA_testing.md)

- [Automated Testing](./Development_Process/Automated_Testing.md)
- [Large Language Model (LLM) for Testing and Debugging](./Development_Process/LLM_Testing_Debugging.md)

### [Getting Started With Docker](./Development_Process/Docker.md)

### [Getting Started With WSL 2](./Development_Process/WSL.md)
### [Setting up Conda for multiple Python environments](./Development_Process/Conda/Setup_Conda.md)

## Nginx

### [Introduction to Nginx](./Development_Process/Nginx.md)

## Build requirements

### [Requirements.txt](./Development_Process/Build_Requirements/Requirements_txt.md)

## Build tools
### [Introduction to ```make``` and Makefiles](./Development_Process/Introduction_to_make_and_Makefiles.md)

## React Testing Library

### [React Testing Library](./Development_Process/React_Testing_Library.md)

## URL Sanitization

### [URL Sanitization](./Development_Process/URL_Sanitization.md)

## Design Decisions

### [GraphQL vs. REST: Which API type to use?](./Development_Process/GraphQL_VS_REST.md)

## Serverless Computing

### [Serverless Computing](./Development_Process/Serverless_AWS_Lambda.md)

## SOLID PRINCIPLES:

SOLID is a mnemonic acronym that represents a set of five very important software development principles which lead to code that is easier to read, maintain, and extend, leading to higher-quality software that is easier to evolve over time.

The SOLID principles are:

- Single Responsibility Principle (SRP): A class should only have one cause to change, according to the Single Responsibility Principle (SRP). According to this theory, a class ought to have just one duty, which implies that there ought to be just one motivation for change. This makes the class more understandable, maintainable, and reuseable as well as more flexible.

- Open/Closed Principle (OCP): Software entities (classes, modules, functions, etc.) should be available for extension but closed for modification, according to the available/Closed Principle (OCP). According to this principle, a system should be able to introduce new functionality without requiring changes to the existing code. Interfaces, polymorphism, and generalization are used to accomplish this.

- Liskov Substitution Principle (LSP): Subtypes must be able to be used in place of their parent types. According to this concept, it should be possible to swap out objects from a superclass for objects from a subclass without having any negative effects on the program's correctness. This necessitates abiding by the superclass's compact.

- Interface Segregation Principle (ISP): Clients should not be forced to depend on interfaces they do not use. This principle states that a client should not be forced to implement an interface if it does not use all of the methods defined by the interface. This helps to avoid the creation of fat interfaces, which are interfaces that contain more methods than the client needs.

- Dependency Inversion Principle (DIP): High-level modules should not depend on low-level modules. Both should depend on abstractions. Abstractions should not depend on details. Details should depend on abstractions. This principle suggests that classes should depend on abstractions rather than concrete implementations, which makes the system more flexible and easier to modify.

## Resource that gives examples of the uses cases of SOLID principles

LINK : https://www.youtube.com/watch?v=_jDNAf3CzeY

## Clean Architecture:

A system's design that divides it into logical parts and specifies how those parts may communicate with one another is referred to as clean architecture. The objective is to make the software system easier to design, deploy, operate, and maintain while still keeping as many options open  for as long as possible.

Clean Architecture works on the well-defined division of layers. It is important to understand what the different layers are and which layers are allowed to interact with each other. The independence that clean architecute introduced to the a software system is vital since it reduces dependancies within the system. In clean architecture, the elements of the inner most layers should not have any information about the outermost layers. Anything declared in an outer layer must not be used anywhere within the inner layer of the code.

![image](https://user-images.githubusercontent.com/75923742/227027780-b5fbf347-ff78-49fa-a122-8f9ac4ef53d4.png)

Some of the layers are (Simplified):

- Business Rules:

  - Entity: A component of our computer system that represents a condensed set of critical business rules that are applied to crucial business data.
  - Use Case: Gives specifics on the input the user must supply and the output the system must deliver to the user. Additionally, it includes the processing steps required to create the result.

- Entities: Contains functions, variables, and other structures that hold the main objectives of our application, they must be general and have the highest level of rules.
- Interface Adaptors: Responsible for communicating between the layers, takes data in and transforms it such that it can be sent to lower levels.
- Framworks and Drivers: This section contains frameworks and databases responsible for communicating with the interface adapters.

This is only a simplification of what "Clean Architecture" is; the topic is so vast that there have been texts that have been dedicated to this topic. Some resources that can be beneficial in understanding and clearing up any doubts about the topic have been linked below.

- Text that goes into greater depth about each layer:

  - https://dev.to/rubemfsv/clean-architecture-the-concept-behind-the-code-52do#:~:text=The%20main%20rule%20for%20Clean,elements%20of%20an%20outermost%20layer.

- Article Summarizing Clean Architecture (Examples and Code)

  - https://pusher.com/tutorials/clean-architecture-introduction/

- A very detailed explanation of Clean Architecture by Robert C. Martin or Uncle Bob and his book

   - https://www.youtube.com/watch?v=2dKZ-dWaCiU 
   - https://github.com/ropalma/ICMC-USP/blob/master/Book%20-%20Clean%20Architecture%20-%20Robert%20Cecil%20Martin.pdf 

## Clean coding
### [Code Smells](./Development_Process/Code_Smells.md)
### [Coding and commenting styles](./Development_Process/clean_coding_styling.md)

## Prompt Engineering
### [Basics of Prompt Engineering](./Development_Process/Prompt_Engineering.md)

## Technical Documents
### [Intro to Request for Comments (RFCs)](./Development_Process/Technical_Documents/Intro_to_rfcs.md)
