## E2E Testing with Cypress

- [Cypress Introduction](#cypress-introduction)
- [Why do end to end testing?](#why-do-end-to-end-testing-)
- [Why Cypress?](#why-cypress-)
- [Installation and setup:](#installation-and-setup-)
- [The basics](#the-basics)
- [Best Practices](#best-practices)

# Cypress Introduction

Cypress is mainly used for testing web applications, especially those built in javascript. It provides an interface to programatically test your application, and visually what went wrong (or right) in tests. This page will primarily focus on E2E (end-to-end) testing with cypress rather than component testing.
  
# Why do end to end testing?  
  
[https://circleci.com/blog/what-is-end-to-end-testing/](https://circleci.com/blog/what-is-end-to-end-testing/)

The above link has a good explanation on what end to end testing is and why it should be used. While other types of tests like unit tests or functional tests make sure a single component/module works as expected, an end to end test starts from the perspective of the end user and tries to mimic what an end user would do when accessing your application. 

Cypress very closely mimics a real user, think of it as a robot accessing your website from a browser like a human would, but you can program the robot to interact with your website however you like and programmatically check the output on the screen.

# Why Cypress?

There exist many different testing frameworks online, such as [Selenium](https://www.selenium.dev/), [Jest](https://jestjs.io/), [Mocha](https://mochajs.org/), and more. 

Cypress is most useful for UI, integration and end-to-end testing, so it can be used in tandem with unit testing frameworks like Jest. 

Cypress is built on top of mocha, and uses its framework for tests as well. The main difference is that cypress focuses more on improving client-side and UI tests. 

Selenium is often compared to Cypress, due to it being one of the most popular UI testing frameworks before Cypress was created. One of the biggest differences is that Cypress automatically retries commands while waiting for DOM elements to load properly, helping to prevent [flaky tests](https://www.jetbrains.com/teamcity/ci-cd-guide/concepts/flaky-tests/) and eliminating the need to write wait or sleep helpers that were needed in Selenium. Cypress is also faster and easier to get setup and start creating tests than Selenium. However, Selenium is more flexible, allowing for testing in multiple browsers at a time, and also for writing tests in languages other than javascript. 

# Installation and setup:  
  
Cypress can be automatically installed with [npm](https://www.npmjs.com/): `npm install cypress`

See [https://docs.cypress.io/guides/getting-started/installing-cypress](https://docs.cypress.io/guides/getting-started/installing-cypress) for more details.

To run cypress, we can use the command `npx cypress open` and follow the instructions provided on the UI. 
  
See [https://docs.cypress.io/guides/getting-started/opening-the-app](https://docs.cypress.io/guides/getting-started/opening-the-app) for more details.

# The basics

Cypress has an extremely detailed guide for getting started, explains how to create and run tests, and there is also a lot of information linked as well.

[https://docs.cypress.io/guides/end-to-end-testing/writing-your-first-end-to-end-test](https://docs.cypress.io/guides/end-to-end-testing/writing-your-first-end-to-end-test)

[https://docs.cypress.io/guides/core-concepts/introduction-to-cypress](https://docs.cypress.io/guides/core-concepts/introduction-to-cypress)

I highly recommend reading through the above two links, and the entirety of the core concepts section in the documentation. It gives a thorough introduction on how cypress works and how to use it to test your application.

The first link provides a detailed guide on how cypress commands work and how to read the testing UI. 

The second link provides a guide to most of the commonly used functions in cypress, like how to query for elements, check if they have or not have a specific property, actions such as clicking on buttons or filling out forms, and more. 

# Best Practices

One common use case for cypress (and UI testing in general) is to test responsiveness, does the UI look like it should in different viewports?

While it is possible to duplicate tests, this may cause you to need to repeat large parts of the code to select elements and fill out forms, which has nothing to do with 

It is much easier to use the beforeEach() hook and a cypress context() to bundle viewpoints together. As an example: 
  
```javascript
viewports = [{“name”: “small”, “dim”: [300, 800]}, 
			{“name”: “large”, “dim": [300, 800]]

viewports.forEach(viewport => {
	cy.context(“Viewport” + viewport.name, () => {
		cy.beforeEach(() => {  
			cy.viewport(viewport.dim[0], viewport.dim[1])  
		})  
		//tests go here  
	})
}
```
In tests, you can include snippets of code like  
```javascript
if (viewport.name == ‘small’) {  
	cy.get("@somedivmobileonly").should('exist')
} else if (viewport.name == 'large') {
	cy.get("@somedivmobileonly").should('not.exist')
} 
```

Another common test for responsiveness is checking the alignment of items, for example testing that one element should be above another in a small viewport and beside another in a larger viewport. 

In this case, you should use a closure (described in the [variables and aliases](https://docs.cypress.io/guides/core-concepts/variables-and-aliases) section) to store the first element's position: 

```javascript
cy.get('elem1').then($elem => {
	cy.get('elem2').then($elem2 => {
		let p1 = $elem.position()
		let p2 = $elem2.position()
		if (viewport.name == 'small') {
			expect(p1.top).to.be.greaterThan(p2.top)
			expect(p1.left).to.be.equal(p2.left)
		} else {
			expect(p1.top).to.be.equal(p1.top)
			expect(p1.left).to.be.greaterThan(p1.left)
		}
	})
})
```

Note the use of `expect` instead of `should`, since we are not chaining off of a cypress command we use an assertion instead. See [here](https://docs.cypress.io/guides/references/assertions) for other assertions. 

For more, Cypress provides their own list of best practices here: [https://docs.cypress.io/guides/references/best-practices](https://docs.cypress.io/guides/references/best-practices). I highly recommend reading their guide, if I had known about this before, I would have saved a lot of effort learning the hard way what not to do. 
