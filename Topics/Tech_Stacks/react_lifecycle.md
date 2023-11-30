# React Lifecycle Methods Documentation

This documentation provides an overview of React lifecycle methods, explaining when each method is called and how you can use them in your React components.

## Table of Contents

1. [Introduction](#introduction)
2. [React Component Lifecycle](#react-component-lifecycle)
3. [Mounting Phase](#mounting-phase)
    - [constructor](#constructor)
    - [render](#render)
    - [componentDidMount](#componentdidmount)
4. [Updating Phase](#updating-phase)
    - [static getDerivedStateFromProps](#static-getderivedstatefromprops)
    - [shouldComponentUpdate](#shouldcomponentupdate)
    - [render](#render)
    - [getSnapshotBeforeUpdate](#getsnapshotbeforeupdate)
    - [componentDidUpdate](#componentdidupdate)
5. [Unmounting Phase](#unmounting-phase)
    - [componentWillUnmount](#componentwillunmount)

## Introduction

React components go through a lifecycle, and React provides a set of methods called lifecycle methods that you can override to run code at particular times in the process. It is crucial to understand these methods to build an efficient React application.
## React Component Lifecycle

React components have several lifecycle methods categorized into different phases:

- **Mounting Phase**: When a component is being created and inserted into the DOM (Document Object Model).
- **Updating Phase**: When a component is being re-rendered as a result of changes to either its props or state.
- **Unmounting Phase**: When a component is being removed from the DOM.

## Mounting Phase

### `constructor`

The `constructor` method is called before a component is mounted. It creates the component and initializes states. Also, it can be used to bind event listeners.

```jsx
constructor(props) {
  super(props);
  // Initialize state
  this.state = {
    // your state properties
  };
}
```
### `render`

The `render` method calls on the component to display its UI. This method does not change the state.

```jsx
render() {
  return (
    // JSX representing the component's UI
  );
}
```

### `componentDidMount`

The `componentDidMount` is the final stage of the mounting process. It allows the component to be called after it has been mounted on the DOM. It handles all network requests such as fetching data from an API.

```jsx
componentDidMount() {
  // Perform actions after the component is mounted (network requests)
}
```

## Updating Phase

### `getDerivedStateFromProps`

The `getDerivedStateFromProps` static method is called before a render, and updates the props and state based on the input.

```jsx
static getDerivedStateFromProps(nextProps, nextState) {
  // Update state based on props
  return null; // or returns the updated state
}
```

### `shouldComponentUpdate`

The `shouldComponentUpdate` method returns true if the component needs to re-render and false otherwise. If there are no changes to the props or state, it prevents unnecessary re-renders.

```jsx
shouldComponentUpdate(nextProps, nextState) {
  // Return true if the component should re-render, false otherwise
}
```

### `render`

The `render` method calls on the component to display its UI. This method does not change the state.

```jsx
render() {
  return (
    // JSX representing the component's UI
  );
}
```

### `getSnapshotBeforeUpdate`

The `getSnapshotBeforeUpdate` method captures the information from the DOM before the update phase changes the information. It helps to preserve and synchronize aspects from before the update to the current.

```jsx
getSnapshotBeforeUpdate(prevProps, prevState) {
  // Capture information before the update
  return null;
}
```

### `componentDidUpdate`

The `componentDidUpdate` method is the final method of the update process and is called after the component updates. It updates the DOM accordingly.

```jsx
componentDidUpdate(prevProps, prevState, snapshot) {
  // Perform actions after the component is updated
}
```

## Unmounting Phase

### `componentWillUnmount`

The `componentWillUnmount` method is called right before the component is removed from the DOM. It cleans up the network requests and the subscriptions associated with the component.

```jsx
componentWillUnmount() {
  // Perform cleanup before the component is removed
}
```
