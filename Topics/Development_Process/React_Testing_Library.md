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

## Example (User Login)

The following test is one way to test a successful login action. After pressing the button, the test tries to find a "Logout" button on the screen that should have been rendered. There are many other ways to do this depending on your application screens, but the goal of the test is to detect some change in the screen that only could have occured if the login was successful.

```
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

## Official documentation (with more examples)

For more in-depth information and examples, refer to the official React Testing Library documentation:

- [React Testing Library Documentation](https://testing-library.com/docs/react-testing-library/example-intro)

- [React Testing Library Cheatsheet](https://testing-library.com/docs/react-testing-library/cheatsheet)

- [React Testing Library API - Events](https://testing-library.com/docs/dom-testing-library/api-events)

- [All Testing Library Events - GitHub Repository](https://github.com/testing-library/dom-testing-library/blob/main/src/event-map.js)

- [React Testing Library API - Async](https://testing-library.com/docs/dom-testing-library/api-async/)

- [Jest-Dom matchers documentation](https://github.com/testing-library/jest-dom#custom-matchers)

## Codesandbox Example
You can find runnable examples for many common use cases on Codesandbox. Refer to this example found in the official documentation: [codesandbox example](https://codesandbox.io/s/github/kentcdodds/react-testing-library-examples/tree/main/).

## Conclusion
React Testing Library is a valuable tool for ensuring the reliability and functionality of your React components. By adopting a user-centric testing approach, you can create tests that are more resilient to changes and provide a better understanding of your application's behavior.
