# Writing Clean Code in React

## Table of Contents

1. [Introduction](#introduction)
2. [Naming](#naming)
3. [Component Structure](#component-structure)
4. [Final Remarks](#final-remarks)
5. [Citations](#citations)

## Introduction

Writing clean and efficient React code is essential for building scalable and maintainable applications. Clean code not only enhances readability but also contributes to better collaboration among developers. New developers often encounter common pitfalls such as neglecting proper component structure, overusing state management, and ignoring code organization. By emphasizing the importance of clean React code, developers can foster a codebase that is easy to understand, debug, and extend, ultimately leading to a more enjoyable and productive development experience.

## Naming

When working with React, it is important to follow a consistent naming convention for components, variables, and functions. This helps developers quickly identify the purpose of each component and function, which is especially useful when working with large codebases. The following are some common naming conventions for React:

### Components

Components should be named using PascalCase. For example, a component that renders a button should be named `Button` instead of `button` or `ButtonComponent`. This convention is consistent with the naming of built-in React components such as `div` and `span`.

### Variables and Functions

Variables and functions should be named using camelCase. For example, a variable that stores a user's name should be named `userName` instead of `user_name` or `user-name`, and a function that handles a button click should be named `handleClick` instead of `handle_click` or `handle-click`. This convention is consistent with the naming of built-in React variables such as `onClick` and `onChange` and built-in React functions such as `useState` and `useEffect`.

### State Variables and Setters

State variables should be prefixed with _is_, _has_, or _should_ to denote boolean values and the setters should be prefixed with _set_ followed by the name of the variable. For example, a state variable that stores whether a user is logged in should be named `isLoggedIn` and its setter should be named `setIsLoggedIn`.

### Event Handlers

Event handlers should be named using camelCase and prefixed with _handle_. For example, a function that handles a button click should be named `handleClick` instead of `onClick`.`

### Props

Props should be named using camelCase, similar to variables. Moreover, it is good practice to list props out when defining a component. This helps developers quickly identify the props that a component accepts. For example, a component that renders a button should be defined as follows:

```jsx
const Button = ({ text, onClick }) => {
  return <button onClick={onClick}>{text}</button>;
};
```

Notice that the onClick handler isn't defined in the component, and prop name isn't prefixed by _handle_. This is because the component is only responsible for rendering the button and not handling the button click. The onClick handler should be defined in the parent component that uses the Button component, and _in the parent component_ the event handler that is passed down to the Button component should be prefixed by _handle_. Like in the below example:

```jsx
const ParentComponent = () => {
  const handleClick = () => {
    // handle button click
  };
  return <Button text="Click Me" onClick={handleClick} />;
};
```

### Constants

Constants should be named using uppercase letters and underscores to separate words. For example, a constant that stores user emails should be named `USER_EMAILS` instead of `user-emails` or `userEmails`.

### File Names

File names should be named using PascalCase. For example, a file that contains a component that renders a navbar element should be named `NavbarElement.jsx` instead of `navbarElement.jsx` or `navbar-element.jsx`.

### CSS Classes and Files

CSS classes should be named using kebab-case or camelCase. For example, a class that styles a div that acts as a container for a cards should be named `cards-container` or `cardsContainer` instead of `cards_container`. CSS Files follows the same convention as CSS classes.

As to what you should name your classes, a popular convention is to use the BEM (Block, Element, Modifier) naming convention. This convention is useful for naming classes that are used to style components. It is a pretty big topic in its own right, so to learn more you might want to check out the [getbem.com website](https://getbem.com/introduction/). Look at a quick example below:

```css
/* In this example:
  - login would be the block 
  - submit-button would be the element
  - disabled would be the modifier*/
.login-submit-button--disabled {
  background-color: #ccc;
  color: #fff;
}
```

You will sometimes find 2 dashes for the modifier like above, or an single dash, or even an underscore. These are not a hard rules. Whats important is to be consistent across your codebase.

### Descriptive Naming

Throughout this article, we haven't been using descriptive names for our examples. This is because we wanted to keep the examples short and simple. However, when writing code, it is important to use descriptive names for components, variables, and functions. This helps developers quickly identify the purpose of each component and function. For example, a button that submits a login form should be called `LoginButton` or `LoginSubmitButton` if there are other buttons in the page that it could be confused with. This is especially important when working with large codebases. Take a look at the following example:

```jsx
// This is a bad example
const Button = ({ text, onClick }) => {
  return <button onClick={onClick}>{text}</button>;
};
```

```jsx
// This is a better example
const LoginSubmitButton = ({ submitText, onFormSubmit }) => {
  return <button onClick={onFormSubmit}>{submitText}</button>;
};
```

## Component Structure

When working with React, it is important to follow a consistent component structure. This helps developers quickly identify the purpose of each component and its role in the application. The following are some common principles for structuring React components:

### Break down components

Components should be broken down into smaller components whenever possible. Large components are difficult to understand and debug. It is also easier to reuse smaller components, which avoids code repetition. This essentially goes back to the [Single Responsibility Principle](https://en.wikipedia.org/wiki/Single-responsibility_principle) in software engineering, which states that each component should be in charge of only one function. 'Robert C. Martin, the originator of the term, expresses the principle as, "A class should have only one reason to change"'([Wikipedia](https://en.wikipedia.org/wiki/Single-responsibility_principle)). For example, a component that renders a user profile page should be broken down into smaller components that render the user's name, profile picture, and bio.

### Organize component hierarchy into folders

Components should be organized into folders based on their role in the application. At the highest level inside the components folder, there should be folders for each of the pages in the website. Within each page folder, there should be folders for each of the components that make up the page. The more deeply nested a component is within its page, the deeper it will be in the folder hierarchy. Moreover, test and CSS files should be together with the jsx files. For example, a website that has a home page and a user profile page should have the following folder structure:

```jsx
src
├── components
│   ├── Home
│   │   ├── Navbar
│   │   │   └── ...
│   │   ├── Home.jsx
│   │   ├── Home.test.jsx
│   │   └── Home.css
│   └── Profile
│       ├── ProfileElements
│       │   └── ...
│       ├── Profile.jsx
│       ├── Profile.test.jsx
│       └── Profile.css
├── App.jsx
├── App.test.jsx
└── index.js
```

### Use container components

Containers are useful for styling, since they can be used to wrap multiple components and apply flex or grid properties to them. They can also be responsible for fetching data and passing it down to child components. This helps separate the logic of fetching data from the logic of rendering components. For example, a component that renders a user profile page should be broken down into a container component that fetches the user's data and a child component that renders the user's data. This is also known as the [smart and dumb component pattern](https://medium.com/@dan_abramov/smart-and-dumb-components-7ca2f9a7c7d0), which dates back to class components.

### Try to use fewer States

State management is a powerful tool in React, but it can also be overused. It is important to consider whether a component really needs to be stateful. If data to persist across re-renders, but don't want every update to **cause** a re-render, you might be interested in using useRef hooks instead. Moreover, it is easier to reuse stateless components.

One way to reduce the number of states is to group related states into a single state object. For example, a component that fetches user data from a database can store the user's name, email, and bio in a single state object instead of storing each piece of data in a separate state.

```jsx
// This is a bad example
const [name, setName] = useState("");
const [email, setEmail] = useState("");
const [bio, setBio] = useState("");

// You will also need to update them separately in the handlers
const handleChange = (e) => {
  setName(e.target.value.name);
  setEmail(e.target.value);
  setBio(e.target.value);
};

// Or maybe even separate handlers!
const handleNameChange = (e) => {
  setName(e.target.value.name);
};

const handleEmailChange = (e) => {
  setEmail(e.target.value);
};

const handleBioChange = (e) => {
  setBio(e.target.value);
};
```

```jsx
// This is a better example
const [user, setUser] = useState({
  name: "",
  email: "",
  bio: "",
});

// To update the state, you only need to update the state object
const handleChange = (e) => {
  setUser({ ...user, [e.target.name]: e.target.value });
};

// It is also good to destruct the state object when using it
const { name, email, bio } = user;
```

It is important to note that this is not always the best approach, since it can lead to a bloated state object, and it's also important for everyone working in the codebase to be aware of the individual states that are grouped together in the state object.

State management is a very complex topic that warrants its own article, so to learn more you might want to check out the [React documentation on state and lifecycle](https://react.dev/learn/state-a-components-memory). [This resource](https://oskari.io/blog/stop-react-global-state-part-1) might also be useful to understand the different types of states a component may have.

### Only use Effects when necessary

Effects are useful for performing side effects such as fetching data from a database or subscribing to an event listener, however they increase the complexity of the code and thus must only be used when necessary. If a component only needs to render data, then it should not use an effect. This helps reduce the complexity of the component and makes it easier to debug. Moreover, it is easier to reuse components that do not use effects since they are not tied to a specific effect. Look at the following example taken from the amazing open source course over at [Odin Project](https://www.theodinproject.com/lessons/node-path-react-new-how-to-deal-with-side-effects).

```jsx
import React, { useState } from "react";

export default function AdditionDisplay() {
  const [number1, setNumber1] = useState(0);
  const [number2, setNumber2] = useState(0);

  // This is all unnecessary.

  // const [sum, setSum] = useState(0);
  // useEffect(() => {
  //   setSum(number1 + number2);
  // }, [number1, number2]);

  const sum = number1 + number2;

  return (
    <p>
      {number1} + {number2} = {sum}
    </p>
  );
}
```

### Use React Fragments

React fragments are useful for rendering multiple elements without adding an extra node to the DOM. This is especially useful when rendering lists of elements, or if your component returns a group of components (like when you refactor a big component to follow the Single Responsability Principle). Be aware that it is not a sin to utilize divs, since they are useful for styling and are useful to decouple data fetching like mentioned above, but if you don't need them, then you should use React Fragments instead.

```jsx
// If don't want to add a div to the DOM tree, you could do this!
const List = () => {
  return (
    <>
      <li>Item 1</li>
      <li>Item 2</li>
      <li>Item 3</li>
    </>
  );
};
```

```jsx
// If you need to add properties to the fragment, you can do this!
const List = () => {
  return (
    <React.Fragment key={item.id}>
      <li>Item 1</li>
      <li>Item 2</li>
      <li>Item 3</li>
    </React.Fragment>
  );
};
```

## Final Remarks

Writing clean and efficient React code is essential for building scalable and maintainable applications. Clean code not only enhances readability but also contributes to better collaboration among developers. We have only scratch the surface in this article, but hopefully you have learned some useful tips and tricks to help you write cleaner React code. If you are interested in learning more, you might want to check out the resources in the citation section.

## Citations

- [Linkedin article on naming conventions](https://www.linkedin.com/pulse/react-js-naming-convention-kristiyan-velkov/)
- [Odin Project's amazing open source React course](https://www.theodinproject.com/paths/full-stack-javascript/courses/react)
- [More on BEM](https://getbem.com/introduction/)
- [React documentation on state and lifecycle](https://react.dev/learn/state-a-components-memory)
- [Another good article on clean code](https://www.turing.com/kb/writing-clean-react-code)
- [And yet another one](https://www.linkedin.com/pulse/best-practices-writing-clean-maintainable-react-code-darshaka-srimal/)
- [Greate article on state management](https://oskari.io/blog/stop-react-global-state-part-1)
- [Fireship's video on some of the topics covered here (and more!)](https://www.youtube.com/watch?v=b0IZo2Aho9Y)
- [Good article on file structure](https://medium.com/@kthamodaran/react-8-best-practices-folder-structure-5dbda48a69e)
