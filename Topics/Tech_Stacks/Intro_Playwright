# Playwright: Web Automation Made Easy
## Table of Contents

1. [What is Playwright?](#what-is-playwright)
2. [Setup and Installation](#setup-and-installation)
3. [Scripting](#scripting)
4. [Headless Mode](#headless-mode)
5. [Automatic Waiting](#automatic-waiting)
6. [Browser Context](#browser-context)
7. [Advantages Over Other Solutions](#advantages-over-other-solutions)
8. [Limitations](#limitations)
9. [Citation & Useful Links](#useful-links)

## What is Playwright
Playwright is an open-source end-to-end testing framework developed by Microsoft, designed specifically for testing modern web applications.

Playwright enables automation of user interactions, including clicking on elements, filling in text fields, and more. It behaves like a user, waiting for elements to become actionable before performing actions and retrying assertions. Moreover, it features default parallel test execution which enhances speed therefore making the testing process exceptionally fast while aslo offering great browser support.

## Setup and Installation
To install Playwright run the following command:

```
npm init playwright@latest
```
It will download the browsers needed along with 
```
playwright.config.ts
package.json
package-lock.json
tests/
  example.spec.ts
tests-examples/
  demo-todo-app.spec.ts
```
To run the example tests do 
```
npx playwright test
```

Alternatively, you could install the Playwright extension on VSCode from the marketplace.
<img width="714" alt="Screenshot 2024-03-17 at 3 42 39 PM" src="https://github.com/learning-software-engineering/learning-software-engineering.github.io/assets/113081946/e79ee478-9d94-49af-ab1a-fb53c6e06e5b">

Once installed, open the command panel and type:
```
Install Playwright
```
Select Test: Install Playwright and then choose the browsers you would like to run your tests on. 
<img width="714" alt="Screenshot 2024-03-17 at 3 44 23 PM" src="https://github.com/learning-software-engineering/learning-software-engineering.github.io/assets/113081946/7c2e3fa9-4224-4fc8-b24a-a2e9d20eb8f5">

## Scripting 
Playwright provides an API for scripting interactions with web pages. Here's an example of how to open a browser, navigate to a website, and perform actions:
```
const { chromium } = require('playwright');

(async () => {
  const browser = await chromium.launch(); // Open the browser
  const page = await browser.newPage();

  await page.goto('https://example.com'); // Navigate to desired page
  await page.click('button#submit'); // Perform a click

  const pageTitle = await page.title(); // Extract data from Page

  console.log('Page Title:', pageTitle);

  await browser.close();
})();
```

## Headless Mode
Headless mode means that you are able to run a web browser without a graphical user interface (GUI). This means that the user isn't shown anything visually which makes testing faster and more effecieint. It is both cost-effective in terms of resources and allows for specific tests to be done. Specifically, the browser operates in the background, allowing you to test, and gather data without displaying the browser window.

Most modern browsers, including Google Chrome, Firefox, and Microsoft Edge, support headless mode. Here's how you can use headless mode with Playwright:
```
const { chromium } = require('playwright');

(async () => {
  const browser = await chromium.launch({ headless: true }); // Set the headless option to true
  const context = await browser.newContext();
  const page = await context.newPage();

  await page.goto('https://example.com'); // Navigate to page
  await page.screenshot({ path: 'example.png' }); // Take a screenshot

  await browser.close();
})();

```

## Automatic Waiting
A feature that distinguishes Playwright from other solutions. It involves eliminating unstable tests by ensuring elements are ready before executing actions. Here's an example:
```
const { chromium } = require('playwright');

(async () => {
  const browser = await chromium.launch();
  const context = await browser.newContext();
  const page = await context.newPage();

  await page.goto('https://example.com'); // Navigate to page

  await page.waitForSelector('#nonexistentButton'); // Await each page.waitForSelector sequentially
  await page.waitForSelector('#nonexistentInput');

  await page.click('#nonexistentButton');  // When both selectors are available, perform actions
  await page.fill('#nonexistentInput', 'Hello, World!');

  await browser.close();
})();

```

## Browser Context
Playwright allows the creation of isolated browser contexts to launch different browsers. Here is an example:
```
const { chromium } = require('playwright');

(async () => {
  const browser = await chromium.launch();

  const context1 = await browser.newContext(); // Create the first browser context
  const page1 = await context1.newPage();

  await page1.goto('https://example.com'); // Navigate to a website in the first context
  console.log(await page1.title()); // Output the title of the page in the first context

  const context2 = await browser.newContext(); // Create the second browser context
  const page2 = await context2.newPage();

  await page2.goto('https://www.google.com'); // Navigate to a different website in the second context
  console.log(await page2.title()); // Output the title of the page in the second context

  await browser.close();
})();

```

## Advantages Over Other Solutions
Playwright is a modern solution for automated testing over frameworks like Selenium which may be a bit outdated. Here are some key advantages as higlighted in a blog by Olga Sheremeta on Testomat [Blog Link](https://testomat.io/blog/test-automation-with-playwright-definition-and-benefits-of-this-testing-framework/): 

* Codegen: Allows test creation through user action recording, with the flexibility to write tests in various programming languages.
* Playwright Inspector: Enables step-by-step monitoring of test execution and detailed analysis of interactions.
* Trace Viewer: Facilitates easy debugging of failed tests by providing access to test recordings, allowing navigation through actions and detailed inspection of each step.
* Automatic Waiting: Eliminates unstable tests by ensuring elements are ready before executing actions, a feature that sets Playwright apart.
* Test Tagging: Groups and runs test cases together for organization and fast execution.
* Built-in Reports: Provides various default and customizable reporting options.
* Video and Screenshot Support: Enables the use of visual aids such as photos and video recordings to identify issues quickly.
* Test Retries: Automatically retries failed tests, improving test reliability, especially for intermittent failures.
* Parallel Test Execution: Supports running multiple test processes simultaneously.
* Browser Context Creation: Allows running tests in isolated browser contexts, significantly faster than launching new browsers, contributing to Playwright's reputation for high-speed testing.

## Limitations 
While Playwright is a powerful tool for automating browser tasks and interactions, like any technology, it does have some imitations:

* Resource Intensive: Running a headless browser can consume a significant amount of system resources, especially when dealing with multiple browser instances. 
* Dynamic Web Content: Playwright is excellent for automating static web pages or simple interactions. However, handling highly dynamic web content, such as single-page applications built with complex JavaScript frameworks like React, may require more advanced techniques.
* Performance Trade-offs: While headless mode can offer faster automation compared to running a browser with a GUI, there can still be performance trade-offs, especially when dealing with complex scenarios.

### All code snippets are taken from other sources
## Citation & Useful Links
* [Github Repository for Playwright](https://github.com/microsoft/playwright)
* [Official Documentaion](https://playwright.dev)
* [VSCode Images and Process](https://dev.to/playwright/running-playwright-tests-on-ci-with-github-actions-30ba)
* [Playwright vs Selenium: A Detailed Comparison in 2024](https://research.aimultiple.com/playwright-vs-selenium/)
* [Testomat Blog by Olga Sheremeta](https://testomat.io/blog/test-automation-with-playwright-definition-and-benefits-of-this-testing-framework/)
* [Common Questions](https://stackoverflow.com/questions/tagged/playwright)



