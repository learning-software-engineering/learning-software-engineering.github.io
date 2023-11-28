# Redux Tutorial

## Introduction

This tutorial provides a comprehensive guide to Redux, a popular state management library in JavaScript, ideal for developers familiar with JavaScript and looking to enhance their web application development skills.

<img src="https://redux.js.org/assets/images/ReduxDataFlowDiagram-49fa8c3968371d9ef6f2a1486bd40a26.gif" alt="Redux Conceptual Image" width="600"/>
    

## What is Redux?

Redux is a predictable state container for JavaScript applications. It's used for managing the state of your app in a more predictable and easier-to-debug manner. Redux maintains the state of an entire application in a single immutable state tree, which can't be changed directly. When changes are made, a new object is created and merged with the state.

## Why Do We Use Redux?

Redux is used for several reasons:

- **Predictability**: It makes the state of your app predictable and transparent. Every change is predictable and happens one at a time.
- **Maintainability**: Redux makes the state changes maintainable and easy to understand, which is especially beneficial in large applications with complex state changes.
  + **Single Source of Truth**: Redux maintains the entire state of your application in a single store. This centralized approach ensures that the state is consistent across the app and makes it easier to track and manage state changes.
  + **Immutable State**: In Redux, the state is immutable, meaning it cannot be changed directly.
- **Debugging**: With Redux, it's easier to debug an application as it provides a clear view of when, how, and why your application's state changed.
- **Flexibility**: Redux can be used with any UI layer, and has a large ecosystem of addons.

However, Redux is not always the best choice for state management. It's best suited for large applications with complex state changes. For smaller applications, you can use React's built-in state management. Complexity is subjective, so it's up to you to decide whether Redux is the right choice for your application.

## How to Install Redux

To install Redux, you need to have Node.js and npm (Node Package Manager) installed on your machine. Once you have them, you can install Redux using npm:

```bash
npm install redux
```

For a React application, you will also need to install React-Redux:

```bash
npm install react-redux
```

## Core Concepts

### Store


In Redux, a store is like a central warehouse that holds all the data your application needs. It's responsible for storing this data, updating it based on specific messages called actions, providing the current data to different parts of your application, and notifying them when any data changes. This centralization helps keep your application organized and ensures that the data flows in a predictable and manageable way.

#### 1. `dispatch`

- The `dispatch` method is used to send actions to the Store, which are processed by reducers to update the state.
- Example:
  ```javascript
  // Dispatching an action
  store.dispatch({ type: 'INCREMENT' });
  ```

#### 2. `getState`

- The `getState` method returns the current state held in the Redux Store. It's useful for accessing the state of the application.
- Example:
  ```javascript
  // Accessing the current state
  const currentState = store.getState();
  console.log(currentState);
  ```

#### 3. `subscribe`

- The `subscribe` method allows you to listen for state changes in the Store. It takes a callback function that gets executed whenever the state changes.
- Example:
  ```javascript
  // Subscribing to state changes
  const unsubscribe = store.subscribe(() => 
    console.log('State changed:', store.getState())
  );

  // To unsubscribe from the state changes
  unsubscribe();
  ```


The Store ensures that state is kept consistent across your application.

### Action
In Redux, an action is like a messenger or a note that tells the store what to do. Imagine the application is a command center, and the store is the main database. An action is a message you send to the database to inform it what needs to be done.

Actions are plain JavaScript objects that represent what happened and what needs to change in the application's state. Each action must have a `type` property, which is a string describing how the state should change.

A typical action may look like this:

```javascript
{
  type: 'ADD_TODO',
  text: 'Complete the Redux tutorial'
}
```

Actions are dispatched using the `dispatch` method of the Store.

### Reducer

In Redux, a reducer is a function that decides how the state of your application changes in response to an action. To put it simply, a reducer acts like a director who takes instructions (actions) and updates the state of the application accordingly.


1. **Function**: A reducer is just a JavaScript function. It takes two inputs: the current state and an action.

2. **Decision Maker**: Based on the type of action it receives, the reducer decides how the state should change. It looks at the action type and possibly its additional data (payload), and then determines what the new state should look like.

3. **Pure and Predictable**: Reducers must be pure functions, which means they always produce the same output for the same set of inputs and don't produce side effects (like modifying variables outside the reducer or making API calls). This makes the changes to your app's state predictable and easier to debug.

4. **Returns New State**: After processing an action, the reducer returns a new state. It's important that reducers don't modify the old state directly. Instead, they produce a new state object with the necessary changes. This is in line with the principle of immutability in Redux, which helps in maintaining a clear history of state changes.

A reducer for a to-do application might look like this:

```javascript
function todos(state = [], action) {
  switch (action.type) {
    case 'ADD_TODO':
      return [...state, { text: action.text, completed: false }];
    default:
      return state;
  }
}
```

### State

The state in Redux is the single source of truth for your application. It's divided into three main types:

- **Domain State**: This is the data related to your business domain, like users, products, etc. It's what your application is "about".
- **UI State**: This includes state related to UI, like current active tab, loading states, user interface states like dropdowns being open or closed.
- **App State**: This encompasses state needed globally by the whole app, like user authentication, theme settings, etc. It's the state that is relevant across different parts of your application.

