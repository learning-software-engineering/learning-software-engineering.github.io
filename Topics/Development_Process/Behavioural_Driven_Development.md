## Test Automation with Behvarioual-Driven Development (BDD)

### Introduction to Behavioural-Driven Development (BDD)

Behavioural-driven development (BDD) is a software development approach that uses plain language to create tests for desired feature behaviour. Specifications are defined in accordance with customers before development starts, and these specifications are used as acceptance criteria. 

The tests are written using specific business language in the form "GIVEN ..., WHEN ..., THEN ..." or "WHEN ..., IF ..., THEN ...":
- GIVEN some pre-conditions, WHEN some action occurs, THEN the application should have the desired result.
- WHEN some situation happens, IF some action occurs, THEN the application should have the desired result. 

Behavioural-driven development uses these specifications to create automated tests. Thus, testing ensures that the application behaviour matches the customer's wishes.

### Creating Automated Tests using BDD

Take the following example of a customer requesting an application that uses a login system.

> User Story: a registered user will be able to log in to see the app contents.
>
> Specification:  
> - GIVEN the user is in the login page and not logged in 
> - WHEN the user provides the correct credentials 
> - THEN log them in and allow them to view the home page
>
> Or equivalently:
> - WHEN the user is in the login page and not logged in 
> - IF the user provides the correct credentials 
> - THEN log them in and allow them to view the home page

Given these details from the customer, it is easy to create a unit test for these specifications, and it is easy for both technical and non-technical teams to confirm that this test confirms some desired behaviour. If the application is tested in this way for all specifications, it is easy to see how automated testing under BDD ensures the application aligns with the customer's vision.

As part of clean coding, use the same naming convention across all tests created using BDD. For example, `WhenXThenY` or `when_x_then_y` or `given_x_when_y_then_z`.

### Why choose BDD?

Behavioural-driven development provide benefits in the following categories during the development process.

#### Requirements Gathering

A software team receives more specific requirements using BDD.

For example, instead of receiving a requirement "implement the login feature", the team is provided a specific requirement "when the user is on the login page, if they provide valid credentials, then the application logs them in and opens the home page".

#### New Releases

New features or changes will still meet the acceptance criteria for both previous and new behaviour while using BDD. If any acceptance criteria is not met, then the new changes will cause testing to fail.

Otherwise, guaranteeing that all features work in the way that the customer is looking for becomes a more diffult task. Some repercussions are as follows: 
- customers/users may notice unintended behaviour
- developer may need to run manual tests
- general worry or anxiety about the application's behaviour

#### Testing

It is easier to write tests using BDD because test cases can be derived from specifications approved by the user. The tests also serve as documentation for desired behaviour of a feature.

Otherwise, the developer may need to put more time and effort into creating tests while writing the code to ensure that the tests are useful.

### Resources

The information on this page comes from the following resources:
- [CSC301 Week 9 Lecture Slides](https://q.utoronto.ca/courses/314973/files/28762519?module_item_id=5216884)
- https://cucumber.io/blog/bdd/getting-started-with-bdd-part-1/
- https://www.softwaretestinghelp.com/bdd-framework/

These resources also provide further reading on behavioural-driven development if you wish to learn more.