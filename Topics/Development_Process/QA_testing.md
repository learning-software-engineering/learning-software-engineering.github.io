# QA Testing: What is it? Why should we do it? How do we do it?

## Table of Contents:

1. [Introduction](#introduction-1)
2. [What is Software QA?](#what-is-software-qa-1)
3. [Why should we test?](#why-should-we-test-1)
4. [How to write test cases?](#how-to-write-test-cases-1)
5. [Automated testing](#automated-testing-1)

## Introduction

This article will specifically focus on the testing portion of the development process. It is an essential and often overlooked part of this process and it will explain what software quality assurance or Software QA is, why it is an important part of the development process, how to do it and links to an overview of automated testing (a useful tool in QA). 
At the end of this article, a CSC301 student would have a basic understanding of Software QA and would be able to look into a career in the Software QA field.


## What is Software QA?

[Quality Assurance, Quality Control and Testing - the Basics of Software Quality Management](https://www.altexsoft.com/whitepapers/quality-assurance-quality-control-and-testing-the-basics-of-software-quality-management/)

This paper is likely the greatest paper about software QA, but it is quite long. Here are some of the main definitions and key takeaways:
- In order to make sure the released software is safe and functions as expected, the concept of software quality was introduced. It is often defined as "the degree of conformance to explicit or implicit requirements and expectations".
- The purpose of QA is to set up adequate processes and introduce the standards of quality to prevent errors and flaws in the product. This is slightly different from testing where the purpose is to detect and solve software errors and flaws.
- There are different levels of software testing: component/unit testing, integration testing, system testing, and acceptance testing.

[What does a Software Quality assurance engineer do?](https://www.careerexplorer.com/careers/software-quality-assurance-engineer/)

This article gives a tease of what a software QA engineer is like, the different types of SQA engineers and their duties and responsibilities. It is the right article to figure out if you want a career in this field or if you are interested in QA.

Software QA engineers take the job of encompassing a range of tasks aimed at identifying and addressing issues so that high-quality software products are delivered. They have a series of responsibilities: 

- Test Planning: make plans for the tests that specify the testing strategies, objectives, scopes, and resources required.
- Test Case Design and Execution: Create detailed test cases based on the product being tested and execute these test cases manually.
- Automation Testing: Develop and maintain automated tests to avoid repetitive testing processes.
- Defect Identification and Reporting: Whenever a defect is found in the test process, it should be documented and reported to the development group, so that it can be fixed in time.
- Regression Testing: Make sure that new code changes do not damage existing functionalities.
- Performance Testing: Test software performance with tools like load testing, stress testing, and scalability testing.

QA engineers may have more responsibilities than what's above. Here we are just listing a few.

There are also Different types of Software QA Engineers, each dedicated to a different specialized role. Here are a few of them: 

- Manual QA Tester: Manual QA testers are responsible for manually executing test cases, and play a crucial role in the initial stages of testing.
- Automation QA Engineer: Automation QA engineers create and maintain automated tests. With these automated tools to perform repetitive tasks, they can easily ensure the reliability of software across multiple iterations.
- Performance Testing Engineer: Performance testing engineers need to evaluate the efficiency of software in different conditions.
- Web QA Engineer: Web QA engineers focus on testing web applications and websites. They make sure that the application works well across different web browsers (cross-browser compatibility), different devices (cross-device compatibility), and different window sizes (responsiveness).
- Accessibility Testing Engineer: Accessibility testing engineers ensure that software applications can be accessed by people with different kinds of disabilities.
- Continuous Integration/Continuous Deployment QA Engineer (CI/CD QA Engineers): CI/CD QA engineers focus on integrating quality assurance processes into automated build and deployment pipelines so that the tests can be conducted rapidly.

As we can see from above, QA engineers are more than simply writing automated test cases and doing manual tests one after another. Sometimes they require more knowledge than simply knowing how to code, like the accessibility testing engineers. They are also an important part of delivering a reliable and high-quality product.


## Why should we test?

Testing is a vital part of the software development life cycle.
[This very entertaining video](https://youtu.be/oLc9gVM8FBM) shows what events prompted the creation of software testing and how it has changed. The first few minutes of the video is what I would like to call attention to. It highlights the importance of software testing as far back as 1999 with the "Y2K" problem. Every software engineer should know about this.

There are many reasons why software testing is important. This blog [7 reasons why software testing is important](https://www.indiumsoftware.com/blog/why-software-testing/) summarizes it into 7 different reasons:
- Helps in Saving money: Finding a bug, especially when it is found early in the development process reduces costs considerably.
- Security: Oftentimes software can be vulnerable to attack, or the information of users can be stolen. It is important to avoid this with proper testing.
- Quality of product: The product should function in a complete manner to ensure an effective customer experience.
- Satisfaction of the Customer: This should be the primary objective of the owner and if the customer is not happy then they will use another product.
- Enhance the development process: Quality assurance allows for the developer to find a wide array of scenarios and errors.
- Easy while adding new features: When changing old code it can sometimes break it without the developer knowing. Testing is a great way to give the developer some confidence when adding a new feature.
- Determining the performance of the software: If your application has a low or reduced performance, it will bring a bad reputation in the market. Software testing can help identify these issues before users do.


## How to write test cases?

Most CS undergrad students might have only written automated tests before, so they might know test cases only as they are in unit tests. However, in software development, test cases are not only for automated tests. They are more often used in manual tests. Normally, we design test cases for manual tests and possibly convert them into automated tests later if needed.

[This article](https://www.coursera.org/articles/how-to-write-test-cases) describes how to write test cases. It describes a test case vs test scenario, the various types of test cases and how to write test cases. Here, we will briefly go through the most important things covered in the article. 

First of all, the article provided a very comprehensive 10-step guide for writing test cases:

1. Define the area you want to cover from the test scenario.
2. Ensure the test case is easy for testers to understand and execute.
3. Understand and apply relevant test designs.
4. Use a unique test case ID.
5. Use the requirements traceability matrix in testing for visibility.
6. Include a clear description in each test.
7. Add proper preconditions and postconditions.
8. Specify the exact expected result. 
9. Utilize suitable testing techniques. 
10. Get your test plan peer-reviewed before moving forward.

The article also included a list of popular test case management tools. You may want to have some experience with one or two of them if you are about to engage in writing tests for a large formal project: 

1. [JIRA](https://www.atlassian.com/software/jira)
2. [Juno.one](https://www.juno.one/)
3. [Klaros Test Management](https://www.klaros-testmanagement.com/en/)
4. [QACoverage](https://www.qacoverage.com/)
5. [Qase](https://qase.io/)
6. [SPIRATEST](https://www.inflectra.com/SpiraTest/) by Inflectra
7. [TestFLO](https://marketplace.atlassian.com/apps/1211393/testflo-test-management-for-jira) for JIRA
8. [Testpad](https://testpad.com/)
9. [XQual](https://www.xqual.com/)
10. [Xray](https://www.getxray.app/)
11. [Zephyr Scale](https://marketplace.atlassian.com/apps/1213259/zephyr-scale-test-management-for-jira) for JIRA
12. [Zephyr Squad](https://marketplace.atlassian.com/apps/1014681/zephyr-squad-test-management-for-jira) for JIRA

There are some important takeaways from this article: 

- Test scenarios v.s. test cases: test scenarios often refer to the broader pictures, describing how the user expects to complete with the software. Test cases refer to the details in the test scenarios, such as a specific way that the user may attempt to achieve the goal.
- Who should write the QA test cases: It's best to have people not involved in coding the product write the test cases because it might bring in fresh perspectives.

If you need more help on how to write a test case, here is a [short blog](https://blog.testlodge.com/how-to-write-test-cases-for-software-with-sample/) that's relatively easy to understand. This blog provides visual examples of what a test case should look like, and a [short video](https://www.youtube.com/watch?v=khGa1Rdzd2A) showing step-by-step how to write a test case.

## Automated testing

Automated testing is an important part of QA testing, that involves engineers writing test scripts, and running them to get test results. Since the test scripts can be reused, it's extremely suitable for conducting tests repeatedly over many iterations of a product. Sometimes, there is a dedicated QA team that writes automated tests. Sometimes, the software development team will do the work.

Detailed information about automated testing can be found on [this page](./Automated_Testing.md).
