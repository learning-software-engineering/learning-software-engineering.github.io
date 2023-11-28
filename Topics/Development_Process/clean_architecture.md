# Introduction to Clean Architecture
Clean Architecture is a software engineering ideology that involves clear separation between different levels in the codebase. 
In short, the goal is to write and oraganize our code in such a way that the internal business logic is separated from the outside delivery mechanism (front-end code). 
This results in cleaner and more portable code, making it an excellent choice to make projects scalable.
Robert C. Martin, also known as "Uncle Bob", is credited with coming up with the concept. 
The following is a link to his book on Clean Architecture (as well as a plethora of other software engineering-related concepts): https://github.com/GunterMueller/Books-3/blob/master/Clean%20Architecture%20A%20Craftsman%20Guide%20to%20Software%20Structure%20and%20Design.pdf
### How does Clean Architecture work?
https://betterprogramming.pub/the-clean-architecture-beginners-guide-e4b7058c1165 

(link to where I got the diagrams and sourced these explanations from)

Clean Architecture splits up a project into 4 layers: 
- The outermost layer, called the frameworks and drivers layer, includes software external to our code like frameworks, UI, databsases, external hardware devices etc.
- The second layer, called the interface adapter layer, contains the code that handles UI inputs. This layer can be further split up into 3 common interfaces: *Presenters* (responsible for UI and changing states), *controllers* (the interface containing functions implemeted by the frameworks/external interfaces) and *gateways* (interface responsible for interacting with the database).
- The third layer, called the application business rules layer, contains code that is not exactly the core functionality, but necessary to support all of the use cases of this application. It is in this layer that controllers, presenters and gateways are called so that the any one use case can be satisfied.
- The fourth and final layer, called the enterprise business logic layer, contains the core functionality of the program. This is the layer least prone to changes (which is why it's the inner-most layer). This layer holds *entities*, which are data structures or objects with methods required to implement the business logic (for example, this layer would hold all of the calculation logic for a calculator app).

![image](https://github.com/Dario1031/learning-software-engineering.github.io/assets/113073212/67c5fcc5-bc93-4544-842c-b9372238199d)

With these layers established, the next step is to make sure that all of our dependencies move inwards, that is, no functions/methods of an inner layer can be called in an outer layer. 
Doing this ensures that changes made to outer layers (using a different framework, database, UI etc.) do not require extensive changes in the inner layers, making for very portable code.
The following is an example scenario to better understand how Clean Architecture works exactly:

![image](https://github.com/Dario1031/learning-software-engineering.github.io/assets/113073212/48359d0a-8b31-43af-8571-4571554bf398)

While this seems like a correct control flow, notice the transitions between the presenter, the use cases and then the controller. We are violating the dependency rule! Rather than having our dependencies point only downwards, half of them point up and half of them point down. How do we fix this? *Depencency inversion*.

### Dependency Inversion
This concept is actually one of the SOLID design principles (covered in another wiki entry). In short, this principle states that we can decouple and invert violations to our dependency rule by putting an interface between the two problematic layers. In his book, Uncle Bob states: 
- "High-level modules should not depend on low-level modules. Both should depend on abstractions"
- "Abstractions should not depend on details. Details should depend on abstractions"

Classes in higher levels should use an interface implemnted by the layer below them. This way, "high level classes" (counter-intuitively, the lower layer) do not depend on "low level classes", making our code portable as desired.

![image](https://github.com/Dario1031/learning-software-engineering.github.io/assets/113073212/5a8a2240-1594-49d9-a4d9-70cbb6d1391b)

Moving back to our original example, we can fix the dependency violation by putting interfaces between our problematic layers, so that the higher layers use interfaces defined by the lower ones:

![image](https://github.com/Dario1031/learning-software-engineering.github.io/assets/113073212/ce5f2c6b-e9cc-458d-859c-4705fbe46d7b)

Dependency inversion is sometimes confusing. This video helps to alleviate that confusion in case my explanation did not fully click: https://www.youtube.com/watch?v=9oHY5TllWaU&ab_channel=WebDevSimplified

### Advantages of Clean Architecture
Now that we covered the basics, what is the benefit of subscribing to this software engineering philosophy?
- Every layer is testable separately. As they are all separated, it is easy to test functionalities for each.
- The program is independent of frameworks. You can change to support more recent frameworks on the fly. Also applies to databases.
- UI can change as much as you want. Can be web-based, console-based, really whatever you want it to be.
- Deployment is made simple all the time as it leaves the connection of the layers as the last step in the process.

### Disadvantages of Clean Architecture
As with everything, there can be potential downsides to Clean Architecture. It is important to explore these to make sure that it is the right system for your purposes:
- Increased overhead via multiple abstraction layers. Lots of function calls, objects created and memory allocations may lead to performance issues.
- It can be a bit confusing at times. The heavy reliance on abstraction is not easy to reason about in your head.
- Can be overkill for a smaller project that does not need to scale this well.

### Clean Architecture vs. Other Architectures
- Microservices Architecture - The application is sectioned up into smaller pieces, each with its own corresponding business logic and database storage. In terms of a large, growing project, following Clean Architecture would be a bigger time investment up front but would allow for much more portability and ease of use down the road. Microservices is probably more suited to a smaller project.
- Monolithic Architecture - A more traditional, single-codebase setup for the entire application. Technically, Clean Architecture is a form of Monolithic Architecture with more constraints to facilitate future changes. Again, this is a good choice for a large project but it requires a bit of time to learn how to set up properly. If you choose to not adhere to Clean Architecture (smaller project), a Monolithic system is simpler than a Microservices system. Be warned that it may get messy and hard to port over to different systems/frameworks!

![image](https://github.com/Dario1031/learning-software-engineering.github.io/assets/113073212/d555716f-4da7-4e2f-bdc3-9737eafe4246)


That's all for my quick crash course on Clean Architecture. This is not a comprehensive guide, but rather a quick breakdown of the main principles. Feel free to leave suggestions for any new additions!







