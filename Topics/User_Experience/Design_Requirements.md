# **Design Requirements**

# Table of Contents

### [Introduction](#introduction)
### [Motivation](#motivation)
### [Functional Design Requirements](#functional-design-requirements)
### [Non-Functional Design Requirements](#non-functional-design-requirements)
### [References](#references)
### [Additional Resources](#additional-resources)

## **Introduction**

Design requirements are expressions which outline “what” the desired product should achieve and “how” it should achieve them, corresponding to the usefulness and usability of designs.

The usefulness of a product is addressed by the question “Are we designing the right thing?”, which considers whether this product is needed by users. 

The usability of a product is addressed by the question “Are we designing the thing right?”, which considers whether users are able to use the product.

To achieve this goal, design requirements include specifications related to user interfaces, navigation, visual design, and additional elements which contribute to the satisfaction of end users and overall usability. This makes design requirements an integral part of the user experience.

## **Motivation**

When working with partner clients, scoping the problem that clients want to address and understanding the requirements that their ideal solution entails is very important. Establishing design requirements is highly valuable for CSC301 students, who need to create minimum-viable-products (MVPs) from scratch.

### **1: Client Needs** 

After synthesizing user stories, extracting the functional and non-functional design requirements for any design, whether it is a web-application or mobile application, will allow students to gauge the specific features that they will be working on to create an MVP that accurately addresses client needs.

### **2: Action Items**

The design requirements make sure that regardless of the platform the solution is being presented in, the main problem the clients present is solved and the user needs are met well. They can also be dissected to identify how the requirements match to various front-end, back-end, or database tasks, allowing for students to scope actionable task items.

### **3: Communication**

Accurately defining and documenting requirements makes sure that the communication between team members and clients are not lost and can be referred to later in the project to see if they have been met, especially after usability studies. Benefits include;

- **Clearer communication**: The developer team and the client are on the same page and can identify misunderstandings early on.
- **Asynchronous communication**: With shared understanding and written documentation, certain questions can be addressed asynchronously, to see if a certain feature matches the clients design requirements.
- **Efficiency**: There is less time spent on actively thinking about what the client had wanted. The written documentation can be easily referred to in later processes and can be used to hold clients accountable as well.

## **Functional Design Requirements**

Functional design requirements specify the goals of the desired product. They focus on the “usefulness” of the product.

Examples include;
- The system must enable users to verify their accounts using their phone number.
- The system should support backward and forward navigation in the research article to follow the natural order of sections.
- The system must allow visitors to sign up for the newsletter by inputting their email. 

Functional requirements are not the same as user stories. In fact, user stories can be used to derive design requirements while centering user needs. An [example] (https://www.nuclino.com/articles/functional-requirements) of this is as follows: 

“User story: As an existing user, I want to be able to log into my account.

Functional requirements:
- The system must allow users to log into their account by entering their email and password.
- The system must allow users to log in with their Google accounts.
- The system must allow users to reset their password by clicking on "I forgot my password" and receiving a link to their verified email address.”

## **Non-Functional Design Requirements**

Non-functional design requirements specify the methods used to achieve the goals of the desired product. They focus on the “usability” of the product and provide constraints on the system and its development. 

Examples include;
- The system should ensure security and privacy in the account verification process, adhering to industry standards for data protection and encryption.
- The system should display as much text as possible, without compromising accessibility standards.
- When the user presses the sign-up button, the system should load the confirmation screen in two seconds.

As seen in the examples, non-functional design requirements impose constraints on how the functional requirements are implemented in terms of **performance, security, reliability, scalability, and portability.*

## Conclusion

Design requirements are helpful not only at the beginning, but also throughout the design cycle: when determining which features that you want to implement or prioritize at each reiteration, you assess the possibilities against the design requirements to ensure centering client needs and main functionalities the desired system is trying to achieve. During low-fidelity prototyping such as MVPs, high-fidelity prototyping, and usability studies, the team can assess whether the design requirements were met and what changes can be made at each subsequent step to better address them.

## References

Fanny Chevalier. 2023. Lecture 05.4: Synthesizing Actionable Insights - Design Requirements. CSC318. (November 2023).

Nuclino. A Guide to Functional Requirements (with Examples). Retrieved November 27, 2023 from https://www.nuclino.com/articles/functional-requirements 

## Additional Resources