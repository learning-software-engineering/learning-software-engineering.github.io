## Writing tests with React Testing Library

When writing test suites for React components, it is a good idea to write tests that do not depend on the implementation details of the components (e.g. props, attributes, state, etc.) but rather on what the components are and how they behave. For example, instead of querying an element by its ID attribute, use an accessibility role (e.g. button, list, listitem) or accessibility label. This makes tests less fragile and prone to breaking when small changes in the components are made.

Additionally, it is a good idea to design tests that mimic the way a user would interact with the app. For example, when writing tests for a Login page/component, to test that login is successful on submission of correct credentials, the test should rougly follow the steps:

1. Query text fields (username, password, etc.) using textbox role/label
2. Enter inputs into text fields
3. Query login button using button role/label
4. Fire press on enter button
5. Query for successful login message/home screen component/etc


## Example with React Native

The following test is one way to test a successful login action. After pressing the button, the test tries to find a "Logout" button on the screen that should have been rendered.

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
https://testing-library.com/docs/react-testing-library/example-intro
