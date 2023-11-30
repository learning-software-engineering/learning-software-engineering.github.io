# JavaScript Testing with Jest

## Table of Contents
1. [What is Jest?](#1-what-is-jest)
   - [Introduction to Jest](#introduction-to-jest)
   - [Why use Jest for testing?](#why-use-jest-for-testing)

2. [Installation & Setup](#2-installation--setup)
   - [System Requirements](#system-requirements)
   - [Installing Jest](#installing-jest)
   - [Configuring Jest for your project](#configuring-jest-for-your-project)
3. [Test Cases and Test Suites](#3-test-cases-and-test-suites)
   - [Writing a Test Case](#writing-a-test-case)
   - [Write a Test Suite](#writing-a-test-suite)
   - [Running Tests](#running-tests)
4. [Matchers](#4-matchers)
5. [Additional Resources](#additional-resources)

## 1. What is Jest?

### Introduction to Jest
Testing is fundamental to the development process. Like good documentation, good testing is something all developers wish they had when joining a new project but may not incorporate into their day-to-day code. Tests ensure code reliability and help with maintainability, especially in large codebases. With JavaScript being one of the main programming languages of web development, ensuring that your code works is vital for the users of your web application.

Jest is a popular JavaScript testing framework developed by Facebook/Meta for React, but it can be used for any JavaScript project. Jest focuses on simplicity, speed, and a developer-friendly testing experience. It comes with built-in functionalities like test assertion, mocking, and code coverage, making it a comprehensive solution for testing JavaScript code.

### Why use Jest for testing?
Jest provides several advantages for developers engaged in testing their applications:

- **Zero Configuration:** Jest requires minimal setup, and in many cases, no configuration is needed out of the box.
  
- **Fast and Parallel Testing:** Jest is optimized for speed, allowing developers to run tests in parallel, significantly reducing test execution time.

- **Built-in Mocking:** Jest simplifies the process of mocking dependencies, making it easier to isolate and test components or modules.

- **Snapshot Testing:** Jest introduces the concept of snapshot testing, which enables capturing and comparing snapshots of rendered components, aiding in identifying unexpected changes.

- **Excellent Documentation and Community Support:** Jest has extensive documentation, and being widely adopted, it benefits from an active community, ensuring that developers can find help and resources easily.

## 2. Installation & Setup

### System Requirements
Before installing Jest, ensure that your development environment meets the following requirements:

- **Node.js:** Jest requires Node.js to run. Make sure you have Node.js installed on your machine.

### Installing Jest
#### Using npm
To install Jest for your project using npm:

```bash
npm install --save-dev jest
```
#### Using Yarn
If you prefer Yarn as your package manager, you can install Jest with the following command:

```bash
yarn add --dev jest
```

### Configuring Jest for your project
Add the following to `package.json
```javascript
// package.json
{
  "scripts": {
    "test": "jest"
  }
}
```

For the purpose of the guide, we will use Jest with its default configuration. For more customized setups, you can create a `jest.config.js` file in your project's root directory. 

```javascript
// jest.config.js
module.exports = {
  // config options go here
};
```

## 3. Test Cases and Test Suites

### Writing a Test Case

Writing a test in Jest involves defining a test function using the `test` or `it` keyword. 

```javascript
// _.test.js
test('multiplies two positive numbers', () => {
  expect(multiply(4, 2)).toEqual(8);
});

test('handles division by zero', () => {
  expect(() => divide(10, 0)).toThrow('Cannot divide by zero');
});
```

### Writing a Test Suite

A test suite is a way to group related test cases. It's created using the `describe` function. The first argument to `describe` is a string that describes the test suite, and the second argument is a function that contains the test cases.

```javascript
// math_functions.test.js
describe('Calculator operations', () => {
  test('adds two numbers', () => {
    expect(add(2, 3)).toEqual(5);
  });

  test('subtracts two numbers', () => {
    expect(subtract(5, 3)).toEqual(2);
  });
});
```

#### Nesting Test Suites
You can nest `describes` to create a hierarchical structure. As you'll see in the Running Tests section, you can run tests based on patterns of naming. By grouping tests sensibly, you can test groups selectively and later on use specific setup and teardown for a `describe` block.
```javascript
describe('Calculator', () => {
  describe('Addition', () => {
    test('adds two positive numbers', () => {
      expect(add(2, 3)).toEqual(5);
    });

    test('adds a positive and a negative number', () => {
      expect(add(5, -3)).toEqual(2);
    });
  });

  describe('Subtraction', () => {
    test('subtracts two positive numbers', () => {
      expect(subtract(5, 3)).toEqual(2);
    });

    // ...
  });
});

```

### Running Tests
You can run all Jest tests with the following:

#### Using npm
```bash
npm test
```

#### Using Yarn:

```bash
yarn test
```

#### Running Specific Tests
To run specific tests, you can use the `--test` flag followed by a pattern or a specific test name. For example, to run the division test:

```bash
npm test -- --test='handles division by zero'
```

To run the all Calculator operations tests:
```bash
npm test -- --test='Calculator operations'
```

To run a specific test in Calculator operations:

```bash
npm test -- --test='Calculator operations adds two numbers'
```

## 4. Matchers

The `expect` statement is similar to assertions from other languages. In order to test the value of an expression Jest uses matchers. They compare the expression in the `expect` statement to value within the parentheses based on their self-explanatory name. 

The pattern you'll be using is `expect(expr).[not].matcher(expr)` (You can add `not` to test for the opposite.)

Here's a list of common matchers you might use:

- Equality
   - `toBe` - matches identity
   - `toEqual` - matches value
- Numbers
   - `toBeGreaterThan`
   - `toBeLessThan`
   - `toBeGreaterThanOrEqual`
   - `toBeLessThanOrEqual`
- Strings
   - `toMatch` - a string or regex
- Truthiness (because JavaScript is weird)
   - `toBeNull`
   - `toBeUndefined`
   - `toBeDefined`
   - `toBeTruthy`
   - `toBeFalsy`
- Errors/Exceptions
   - `toThrow`
- Arrays/Iterables
   - `toContain`

## Additional Resources

### [Official Jest Documentation](https://jestjs.io/docs/getting-started)