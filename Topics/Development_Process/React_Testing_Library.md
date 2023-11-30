## Table of Contents
- [Table of Contents](#table-of-contents)
- [Introduction](#introduction)
- [Installation and Setup](#installation-and-setup)
- [Writing tests with React Testing Library](#writing-tests-with-react-testing-library)
- [React Testing Library Resources](#react-testing-library-resources)
- [Example (User Login)](#example-user-login)
- [Codesandbox Example](#codesandbox-example)
- [Conclusion](#conclusion)

## Introduction
React Testing Library is a powerful tool for testing React components. It emphasizes writing tests that focus on user behavior rather than implementation details. This ensures that your tests remain robust even when components undergo refactoring changes. Jest and React Testing Library are both commonly used testing tools in the React ecosystem, but they serve different purposes, and often are used alongside one another. Jest might be used for testing utility functions, APIs, and other non-React-specific parts of an application. React Testing Library would be used for testing the actual React components, focusing on how they interact with the DOM and ensuring a user-centric approach.

**Key Principles:**
- **User-Centric Testing:** Write tests that reflect user interactions and expectations rather than relying on component implementation details.
- **Accessibility-Driven Testing:** Emphasize testing based on accessibility roles, labels, and attributes.

## Installation and Setup

If you are using Create React App, Jest and React Testing Library are preconfigured. You can start writing tests without additional setup. Otherwise, see the full setup guide [here](https://testing-library.com/docs/react-testing-library/setup).


**Install React Testing Library:**
Run the following command to install React Testing Library as a dependency:
```
npm install --save-dev @testing-library/react
```

**Install Jest (if not already installed):**

If you haven't set up Jest for your project, you may need to install it as well:

```
npm install --save-dev jest
```

## Writing tests with React Testing Library

When constructing test suites for React components, it is crucial to craft tests that are resilient to changes in implementation details such as props, attributes, and state. Rather than relying on specific attributes like ID, the emphasis should be on understanding the components' nature and behavior. A recommended practice is to use accessibility roles (e.g., button, list, listitem) or accessibility labels for element queries. This approach makes tests less prone to fragility, ensuring they remain robust in the face of minor component modifications.

Furthermore, test design should closely mimic the way a user interacts with the application. For instance, when creating tests for a Login page or component, the test scenario should approximately follow these steps:

1. Querying Text Fields:
	- Utilize accessibility roles or labels to query text fields such as username and password.

2. Entering Inputs:
	- Simulate user input by entering relevant data into the text fields.

3. Querying Login Button:
	- Identify the login button using its accessibility role or label.

4. Triggering Login Action:
	- Simulate the user pressing the enter button to trigger the login action.

5. Verification Steps:
	- Query for elements indicative of a successful login, such as a success message or the appearance of the home screen component.

By structuring tests in this user-centric manner, developers ensure that the tests not only verify the correctness of the components but also validate their functionality from an end-user perspective. This approach enhances the adaptability of tests to changes in the application's behavior and promotes the creation of more meaningful and reliable test suites.

## React Testing Library Resources

To enhance your testing capabilities with React Testing Library, it's beneficial to explore specific resources that provide detailed information on queries, event simulation, and handling asynchronous code:

1. Querying Elements:
	- When seeking optimal methods for querying elements on the page, refer to the React Testing Library Cheatsheet for Queries available at: [React Testing Library Cheatsheet for Queries](https://testing-library.com/docs/react-testing-library/cheatsheet/#queries)
	- Examples:
		- **getByText** *(find by element text content)*
		- **findAllByPlaceholderText** *(find by input placeholder value)*
		- **queryByRole** *(find by aria role)*

2. Simulating User Interaction:
	- For simulating user interactions, such as clicking, typing, and toggling, explore the API documentation on firing events: [React Testing Library API - Events](https://testing-library.com/docs/dom-testing-library/api-events)
	- Additionally, for a comprehensive list of events supported, visit the event map repository on GitHub: [All Testing Library Events - GitHub Repository](https://github.com/testing-library/dom-testing-library/blob/main/src/event-map.js)
	- Examples:
		- **fireEvent.keyDown(domNode, {key: 'Enter', code: 'Enter', charCode: 13})** *(type a key)*
		- **fireEevent.click(domNode)** *(click an element)*

3. Handling Asynchronous Code:
	- When dealing with asynchronous code and waiting for specific changes or events, refer to the asynchronous documentation in the React Testing Library API: [React Testing Library API - Async](https://testing-library.com/docs/dom-testing-library/api-async/)

4. Matchers (Assertions):
	- For assertions in your tests, including custom matchers, refer to the [Jest-Dom documentation](https://github.com/testing-library/jest-dom#custom-matchers) for a comprehensive guide on available matchers and their usage.
	- Examples:
		- **toBeInTheDocument()** *(assert whether an element is present in the document or not)*
		- **toHaveStyle(css: string | object)** *(check if a certain element has some specific css properties)*
		- **toHaveTextContent(text: string | RegExp, options?: {normalizeWhitespace: boolean})** *(check whether the given node has a text content)*

For more in-depth information and examples, refer to the official React Testing Library documentation:

- [React Testing Library Documentation](https://testing-library.com/docs/react-testing-library/example-intro)

- [React Testing Library Cheatsheet](https://testing-library.com/docs/react-testing-library/cheatsheet)


## Example (User Login)

The following test is one way to test a successful login action. After pressing the button, the test tries to find a "Logout" button on the screen that should have been rendered. There are many other ways to do this depending on your application screens, but the goal of the test is to detect some change in the screen that only could have occured if the login was successful.

```
import React from 'react';
import { render, screen } from '@testing-library/react';
import App from './App';

it("should redirect to home page when logged in successfully", async () => {
	render(<App />);
	const emailField = screen.getByLabelText("Email");
	const passwordField = screen.getByLabelText("Password");
	const loginButton = screen.getByRole("button", { name: "Login" });

	fireEvent.changeText(emailField, 'user@email.com');
	fireEvent.changeText(passwordField, 'user');
	fireEvent.press(loginButton);

	const logoutText = await screen.findByText("Logout");
	expect(logoutText).toBeVisible();
});
```

## Codesandbox Example
You can find runnable examples for many common use cases on Codesandbox. Refer to this example found in the official documentation: [codesandbox example](https://codesandbox.io/s/github/kentcdodds/react-testing-library-examples/tree/main/).

## Conclusion
React Testing Library is a valuable tool for ensuring the reliability and functionality of your React components. By adopting a user-centric testing approach, you can create tests that are more resilient to changes and provide a better understanding of your application's behavior.
