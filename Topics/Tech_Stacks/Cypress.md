## E2E Testing with Cypress

# Cypress Introduction

Cypress is mainly used for testing web applications, especially those built in javascript. It provides an interface to programatically test your application, and visually what went wrong (or right) in tests. 
  
# Why do end to end testing?  
  
[https://circleci.com/blog/what-is-end-to-end-testing/](https://circleci.com/blog/what-is-end-to-end-testing/)

The above link has a good explanation on what end to end testing is and why it should be used. 

Cypress very closely mimics a real user, think of it as a robot accessing your website from a browser like a human would, but you can program the robot to interact with your website however you like and programmatically check the output on the screen.

# Installation and setup:  
  
Cypress can be automatically installed with npm: `npm install cypress`

See [https://docs.cypress.io/guides/getting-started/installing-cypress](https://docs.cypress.io/guides/getting-started/installing-cypress) for more details.

To run cypress, we can use the command `npx cypress open` and follow the instructions provided on the UI. 
  
See [https://docs.cypress.io/guides/getting-started/opening-the-app](https://docs.cypress.io/guides/getting-started/opening-the-app) for more details.

# The basics

Cypress has an extremely detailed guide for getting started, explains how to create and run tests, and there is also a lot of information linked as well.

[https://docs.cypress.io/guides/end-to-end-testing/writing-your-first-end-to-end-test](https://docs.cypress.io/guides/end-to-end-testing/writing-your-first-end-to-end-test)

[https://docs.cypress.io/guides/core-concepts/introduction-to-cypress](https://docs.cypress.io/guides/core-concepts/introduction-to-cypress)

I highly recommend reading through the above two links, and the entirety of the core concepts section in the documentation. It gives a thorough introduction on how cypress works and how to use it to test your application.

# Best Practices

Cypress provides their own list of best practices here: [https://docs.cypress.io/guides/references/best-practices](https://docs.cypress.io/guides/references/best-practices)

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
```
if (viewport.name == ‘small’) {  
	cy.get("@somedivmobileonly").should('exist')
} else if (viewport.name == 'large') {
	cy.get("@somedivmobileonly").should('not.exist')
} 
```
