# React Components

## What Are Components In React?
React Components refer to independent and reusable chunks of code that encapsulate a specific functionality or UI that can be imported and used in a larger application. Essentially, React Components serve a similar purpose as JavaScript functions but for front-end UI contexts as they work in isolation, can be given an input, and return an HTML graphical component for the user to conveniently use as a cog in their larger web application. In total, this allows you to split the UI of your application into modular, reusable pieces, and focus on each piece in isolation to create a powerful application.

## When To Use React Components?
It is a best practice for React developers to define and use a React component whenever defining UI code that may be repeated again in their project. Looking back to our analogy with javaScript functions, this is similar to encapsulating a for loop and some calculations into a function so that we don’t have to repeat this same piece of code several times in our project, following the SOLID design principles.
Understanding this purpose, here are a couple of examples of UI parts that could warrant the use of a React Component on a typical web application:
- Page Formatting Basics: Header, Footer, Sidebar, etc
- Functionality: Buttons, Forms, Dropwdowns, etc
- Other: Alerts, Progress bar, Notifications, etc

## Why Use React Components?
Although they are not necessarily required for basic functionality, it is a best practice for software developers to use React components whenever a piece of code in the UI serves an independent purpose and can be abstracted away. The benefits of using React Components include:

- **Modularity:** React components promote modularity, which is in general a best practice in software engineering to break down the interface into smaller components and focus on each one directly, making it easier to manage, debug, and extend features in large-scale projects.
- **Reusability:** With React components, you can create reusable UI elements that can be imported onto any page and used to reproduce the same interface. Thus, we reduce the redundancy in our projects and improve efficiency by not needing to rewrite the same code, we can simply pass in the parameters or props that we would like for the component and reuse in whatever context we want.
- **Hierarchical Organization:** Using React components, we can nest certain components as subparts of others (stylised buttons in a drop down), enhancing our projects organisation as a developer can clearly see how a complex UI interface is broken down into subcomponents, and how those subcomponents are formed in their finest parts, which can help build something a new from it.

## Class Components VS Functional Components
React components come in two flavours, class components and functional components, which essentially differ by their ability to manage internal state.

### Class Components
- **Stateful Components:** Have the ability to hold and manage local state
- `this.state:` Used to access local state.
- `this.setState():` Used to update local state.
- Can maintain their own private data and are more feature rich.
- Useful for complex UI logic involving managing dynamic data that can change over time based on user interactions or other factors.
- Provide lifecycle hook which are special methods that provide the ability to perform specific tasks at different stages in the life cycle of a component.
  - `componentDidMount`
  - `componentDidUpdate`
  - `componentWillUnmount`
- Can update their own state and trigger a re-render.

**Class Component Code Example:**
- In this example we have a simpler number counter which a button to increment the count
- We display the count at the bottom with the button to increment counter
```jsx
import React, { Component } from 'react';

class Counter extends Component {
  constructor(props) {
    super(props);
    this.state = {
      count: 0, // Initializing the state with a count of 0
    };
  }

  incrementCount = () => {
    this.setState({ count: this.state.count + 1 }); // Updating the count in the state
  };

  render() {
    return (
      <div>
        <p>Count: {this.state.count}</p> {/* Displaying the current count */}
        <button onClick={this.incrementCount}>Increment</button> {/* Button to increment the count */}
      </div>
    );
  }
}

```

### Functional Components
- **Stateless Components:** Do not have the ability to hold and manage local state.
- Simpler and more lightweight compared to class components.
- Absence of the `this` keyword.
- Ideal for purely presentational aspects of a web application.
- Can take `props` as a parameter and use them in the HTML response.
- Tip: Use Func components as much as possible for graphical components

**Functional Component Code Example:**
- In this example we simply return an html response with the name that was provided in props
- Note that we “export default <functionalCompName>” at the end to import it from another file 

```jsx
import React from 'react';

const FunctionalComponent = (props) => {
  return (
    <div>
      <h1>Hello, {props.name}!</h1>
      <p>This is a functional component.</p>
    </div>
  );
};

export default FunctionalComponent;
```

## Managing State With Functional Components: `useState` Hooks
Although Functional Components do not inherently allow for local state to be managed, React Hooks makes this possible. Here is an example of a useState hook:
- Ex: ```jsx const [count, setCount] = useState(0); ```
- count: variable name and source of value
- setCount: the setter function which sets count to that new value in the brackets (ex: setCount(5), now count = 5)
- useState(0): define initial value of count to be 0

**Example of `useState` Hook:**
- This is a similar example to what we had in the class component example but this time implemented with a functional component and a useState hook 

```jsx
import React, { useState } from 'react';

const Counter = () => {
  const [count, setCount] = useState(0);

  const increment = () => {
    setCount(count + 1);
  };

  return (
    <div>
      <p>Count: {count}</p>
      <button onClick={increment}>Increment</button>
    </div>
  );
};
```

# Final Remark
With the introduction of `useState` hooks, functional components can now manage their internal state, side effects, and other advanced features, making them more powerful and versatile for smaller components. However, for projects involving advanced state management and more complex components, it's recommended to use class components.

## Sources
- [Understanding Stateful and Stateless Components in ReactJS](https://medium.com/@darshana_18428/understanding-stateful-and-stateless-components-in-reactjs-8f7cee2bf43e)
- [React Components - W3Schools](https://www.w3schools.com/react/react_components.asp#:~:text=Components%20are%20independent%20and%20reusable,will%20concentrate%20on%20Function%20components.)
- [React Components and Props - React Documentation](https://legacy.reactjs.org/docs/components-and-props.html)
- [Building Reusable Components Using React](https://buttercms.com/blog/building-reusable-components-using-react/)

