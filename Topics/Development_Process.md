## Resources for Development Process

## Git

### [Learning Git](./Development_Process/Git/Git.md)

### [Trunk-Based Development](./Development_Process/Trunk_Development.md)

### [Django Project Deployment: AWS, Vercel, and Railway](./Development_Process/Django_Deployment_AWS_Railway_Vercel.md)

### [Node.js Project Deployment: Azure](./Development_Process/Azure_webapp_deployment_with_nodejs.md)

### [Automated Frontend Deployment with Vercel](./Development_Process/Frontend_Automated_Deployment_Vercel.md)

### [Flask Application Deployment on Heroku](./Development_Process/Flask_App_Deployment_Heroku.md)
### [NextJS Deployment on AWS](./Development_Process/NextJS_AWS_Deployment.md)

### [iOS App Deployment onto the App Store](./Development_Process/App_Store_Deployment.md)

### [Quality Assurance Testing](./Development_Process/QA_testing.md)

- [Automated Testing](./Development_Process/Automated_Testing.md)
- [Automated Testing with Behavioural-Driven Development (BDD)](./Development_Process/Behavioural_Driven_Development.md)
- [Large Language Model (LLM) for Testing and Debugging](./Development_Process/LLM_Testing_Debugging.md)

### [Getting Started With Docker](./Development_Process/Docker.md)

### [Getting Started With WSL 2](./Development_Process/WSL.md)

## Accessing your Project

### Nginx

#### [Introduction to Nginx](./Development_Process/Nginx.md)

### Caddy

#### [Getting Started with Caddy](./Development_Process/Caddy.md)

### DuckDNS

#### [Overcoming Dynamic IPs with DuckDNS](./Development_Process/Duckdns.md)

## Build requirements

### [Requirements.txt](./Development_Process/Build_Requirements/Requirements_txt.md)

### [CMakeLists.txt](./Development_Process/Build_Requirements/CMakeLists_txt.md)

## Github Actions

### [Introduction to Github Actions](./Development_Process/Github_Actions.md)


## Build tools
### [Introduction to ```make``` and Makefiles](./Development_Process/Introduction_to_make_and_Makefiles.md)
### [Introduction to Jenkins](./Development_Process/Jenkins/Jenkins.md)
### [Introduction to the Gradle build tool](./Development_Process/Gradle_build_tool.md) 


## Testing Frameworks

### [React Testing Library](./Development_Process/React_Testing_Library.md)

### [Intro to Jest for JavaScript](./Development_Process/Intro_to_Jest.md)

## URL Sanitization

### [URL Sanitization](./Development_Process/URL_Sanitization.md)


## Code Quality

### [Developing With SonarQube](./Development_Process/SonarQube.md)

## Test Driven Development

### [Intro to Test Driven Development](./Development_Process/Test_Driven_Development.md)

## Design Decisions

### [GraphQL vs. REST: Which API type to use?](./Development_Process/GraphQL_VS_REST.md)

### [Graceful Error Handling in Express](./Development_Process/Error_Handling_in_ExpressJS.md)

## Serverless Computing

### [Serverless Computing](./Development_Process/Serverless_AWS_Lambda.md)

### [Azure Functions](./Development_Process/Azure_Functions.md)

## Introduction to Shells

### [Introduction to using Shell](./Development_Process/Shell/intro_to_shell.md)

## Environment

### [Managing Environment Variables and Secrets](Development_Process/Managing_Environment_Variables_and_Secrets.md)

## SOLID PRINCIPLES:

SOLID is a mnemonic acronym that represents a set of five very important software development principles which lead to code that is easier to read, maintain, and extend, leading to higher-quality software that is easier to evolve over time.

The SOLID principles are:

#### Single Responsibility Principle (SRP): 
- A class should only have one cause to change, according to the Single Responsibility Principle (SRP). According to the Single Responsibility Principle (SRP), each class or module should focus on a single concern, ensuring ease of understanding and modification. 

- **Advantage**:  This principle promotes maintainability by isolating responsibilities, reducing potential bugs caused by interconnected changes. Each class or module focuses on a single concern, making it easier to understand, test, and modify. 

#### Open/Closed Principle (OCP)
- Software entities (classes, modules, functions, etc.) should be available for extension but closed for modification, according to the available/Closed Principle (OCP). It means system should be able to introduce new functionality without requiring changes to the existing code. Interfaces, polymorphism, and generalization are used to accomplish this.

- **Advantage**: OCP achieves stability by encouraging developers to create adaptable and scalable systems that accommodate changes through extensions rather than direct modifications. This promotes a more stable codebase and reduces the risk of introducing bugs in previously functioning code.

#### Liskov Substitution Principle (LSP)
-  Subtypes must be able to be used in place of their parent types. According to this concept, it should be possible to swap out objects from a superclass for objects from a subclass without having any negative effects on the program's correctness. This necessitates abiding by the superclass's compact.

- **Advantage**: This principle fosters code reusability and allows for easier substitution of objects within the same inheritance tree. It simplifies maintenance, reducing the need for extensive modifications when introducing new objects or making alterations within the hierarchy. It ensures that system evolution remains agile and manageable without causing extensive disruptions to the existing codebase.

#### Interface Segregation Principle (ISP)
- This principle suggests that clients should not be forced to depend on interfaces they do not use. Instead of one large interface, it's better to have multiple smaller, specific interfaces that cater to the exact needs of the clients.

- **Advantage**: Promotes flexibility and avoids unnecessary dependencies. This helps to avoid the creation of fat interfaces, which are interfaces that contain more methods than the client needs. Ultimately, ISP encourages a modular and precise approach to interface construction, contributing to better software architecture and maintainability.

#### Dependency Inversion Principle (DIP)
- High-level modules should not depend on low-level modules. Both should depend on abstractions. Abstractions should not depend on details. Details should depend on abstractions. This principle suggests that classes should depend on abstractions rather than concrete implementations, which makes the system more flexible and easier to modify.

- **Advantage**: Encourages loose coupling and easier maintenance of the system. This facilitates easier modifications, replacements, and testing, as changes in low-level modules don’t affect the higher-level ones.

## Restaurant example of each principle

#### SRP
Consider a **Chef** in a restaurant. Initially, the chef might handle multiple responsibilities: preparing dishes, managing inventory, and overseeing kitchen hygiene. Adhering to SRP, distinct roles are established. The chef focuses solely on cooking, while inventory management becomes the responsibility of a dedicated inventory manager. 

#### OCP
Suppose a restaurant offers a fixed menu, and every addition or modification requires altering the entire menu preparation process. Adhering to OCP, the menu system can be designed with a base menu class that remains closed for modification. New dishes or changes are introduced via an extension, such as a SpecialsMenu class, allowing additions without altering the existing menu. This principle enables the restaurant to introduce seasonal or daily specials without affecting the core menu.

#### LSP
Imagine a scenario where the restaurant's system expects all orders to be instances of a generic Order class. Adhering to LSP, any specialized order, like a delivery order, dine-in order, or takeaway order, should be substitutable for a standard order without breaking the system's functionality. Each specific order type should adhere to the expected behavior of the generic Order class, ensuring seamless substitution.

#### ISP
Consider a system where all employees (servers, chefs, and cleaners) are expected to use the same comprehensive Employee interface, including methods for serving tables, cooking dishes, and cleaning. Adhering to ISP, distinct interfaces are established for each role: ServerInterface, ChefInterface, and CleanerInterface. This segregation ensures that each role implements only the methods relevant to their responsibilities, preventing unnecessary method implementations.

#### DIP
Suppose the restaurant's ordering system directly depends on specific external services for payment processing and inventory updates. Adhering to DIP, the system can depend on abstract interfaces like PaymentProcessor and InventoryService, allowing flexibility to switch between different payment processors or inventory management systems without directly impacting the core ordering system. This abstraction and dependency on interfaces rather than concrete implementations facilitate adaptability and system maintenance.


## Resource that gives example of actual code of SOLID principles

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

## Code Smells

### [Code Smells](./Development_Process/Code_Smells.md)

## Clean coding
### [Coding and commenting styles](./Development_Process/clean_coding_styling.md)

## Prompt Engineering
### [Basics of Prompt Engineering](./Development_Process/Prompt_Engineering.md)


## Technical Documents
### [Intro to Request for Comments (RFCs)](./Development_Process/Technical_Documents/Intro_to_rfcs.md)


### [API documentation with SwaggerHub](./Development_Process/Documentation/Swagger_API_Documentation.md)

## Ubuntu Server Edition 20.04

### [Guide for setting up a home server with Ubuntu Server Edition](./Development_Process/ubuntu.md)