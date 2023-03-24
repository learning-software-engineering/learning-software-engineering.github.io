### Automated Testing

Automated testing is an important part of industry software engineering development, and is
virtually present at all major companies. While in certain companies, this role will be covered by a
dedicated QA team, in others, it will be the responsibility of the developers themselves, e.g., at
Amazon. Regardless, understanding and being able to write unit tests is important for a SWE to be
able to communicate and standby their code.

The automated testing process is part of the wider build/development process and is usually run as
part of the CI/CD pipeline. The ultimate goal of automated testing is to ensure that the code
functions as expected, and that any changes to the codebase do not break existing functionality.

As background, most companies to implement their CI/CD pipeline with their Git implementation (of
which are usually internal), and so we will be talking about unit testing and integration testing
from the point of you pushing your code to a Git repository. So imagine that all of these tests will
be executed from the moment that you push your code to your project repository.

Further, there are usually "pipelines" for each project (e.g.,
[AWS CodePipeline](https://docs.aws.amazon.com/codepipeline/latest/userguide/welcome-introducing.html)),
and each of your code commits "flows" through your project pipeline. Generally, pipelines are
usually composed of a series of "stages" that are executed sequentially. For example, after some
cloud machine builds your code, the first testing stage might be to run the unit tests, and the
second testing stage might be to run the integration tests. These setups vary from project to
project, and you may be able to override passing criteria, but testing can lead credence to your
implementation, and can support allow your code to promote (pass on to) production.

![AWS CodePipeline Diagram](https://docs.aws.amazon.com/images/codepipeline/latest/userguide/images/pipeline-elements-workflow-application.png)

#### Unit Testing

Unit tests are meant to test your code commit(s) specifically, rather than dependencies and other modules that
may be present in the code base. So unit tests go well with the
[microservices architecture](https://learn.microsoft.com/en-us/azure/architecture/guide/architecture-styles/microservices).
The industry will use various frameworks for unit testing, depending on the stack, e.g., language.
For example, Python uses [unittest](https://docs.python.org/3/library/unittest.html), Java uses
[JUnit](https://junit.org/junit5/) or [Mockito](https://site.mockito.org/), and
JavaScript/TypeScript uses [Jest](https://jestjs.io/). A good choice is one that supports mocking,
spies, and other features that allow you to avoid testing 3rd party function calls (don't run them).
Instead you should assume some expected behaviour from 3rd party function calls, and write tests
that cover every "branch" of your code (code coverage). With that stated, some resources for the
most important parts of unit testing are:

-   **Test Coverage**:
    - Atlassian: [What is Test Coverage?](https://www.atlassian.com/continuous-delivery/software-testing/code-coverage)
    - Microsoft: [Code Coverage](https://learn.microsoft.com/en-us/visualstudio/test/using-code-coverage-to-determine-how-much-code-is-being-tested?view=vs-2022&tabs=csharp)
-   **Unit Test Cases**:
    -   Guru99: [Unit Testing Tutorial](https://www.guru99.com/unit-testing-guide.html)
    -   AWS Unit Testing: [Getting started with testing serverless applications](https://aws.amazon.com/blogs/compute/getting-started-with-testing-serverless-applications/)
    -   Coursera: [How to Write Test Cases: A Step-by-Step QA Guide](https://www.coursera.org/articles/how-to-write-test-cases)
-   **Mocking**:
    -   Mocking in Python: [Mocking in Python](https://realpython.com/python-mock-library/)
    -   Mocking in Java: [Mockito Tutorial](https://www.vogella.com/tutorials/Mockito/article.html)
    -   Mocking in JavaScript: [A guide to module mocking with Jest](https://www.emgoto.com/mocking-with-jest/)

#### Integration Testing

Integration testing, in contrast to unit testing, is meant to verify that your code works with other components/modules/services. We want to test that overall the entire system works as expected. They often execute after setting a production-like environment, and integration test frameworks can differ between projects, but while there aren't really any ubiquitous integration testing specific frameworks, services like CircleCI can help automate the process, and [Selenium](https://www.selenium.dev/) is a popular tool for testing web applications. Some resources for the most important parts of integration testing approaches are:

-  **General**:
   -  Guru99: [Integration Testing Tutorial](https://www.guru99.com/integration-testing.html)
   -  Educative: [What are the different approaches to integration testing?](https://www.educative.io/edpresso/what-are-the-different-approaches-to-integration-testing)
-   **Big Bang Approach**:
    -   Educative: [What is big bang testing?](https://www.educative.io/edpresso/what-is-big-bang-testing)
-   **Incremental Approach**:
    -   Educative: [What is incremental testing?](https://www.educative.io/edpresso/what-is-incremental-testing)
-   **Sandwich/Hybrid Approach**:
    -   Educative: [What is the hybrid testing approach?](https://www.educative.io/answers/what-is-hybrid-integration-testing)