# Redux Tutorial

## Introduction

This tutorial provides a comprehensive guide to Redux, a popular state management library in JavaScript, ideal for developers familiar with JavaScript and looking to enhance their web application development skills.

<img src="https://redux.js.org/assets/images/ReduxDataFlowDiagram-49fa8c3968371d9ef6f2a1486bd40a26.gif" alt="Redux Conceptual Image" width="600"/>

## Table of Contents

- [Redux Tutorial](#redux-tutorial)
  - [Introduction](#introduction)
  - [Table of Contents](#table-of-contents)
  - [What is Redux?](#what-is-redux)
  - [How to Install Redux](#how-to-install-redux)
  - [Core Concepts](#core-concepts)
    - [Store](#store)
    - [Action](#action)
    - [Reducer](#reducer)
    - [State](#state)

    

## What is Redux?

Redux is a predictable state container for JavaScript applications. It's used for managing the state of your app in a more predictable and easier-to-debug manner. Redux maintains the state of an entire application in a single immutable state tree, which can't be changed directly. When changes are made, a new object is created and merged with the state.

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

The Store is the central hub where all application state is stored. It's created using Redux's `createStore` method. The Store provides several methods:

- `dispatch`: Used to dispatch actions to the Store.
- `getState`: Returns the current state held in the Redux Store.
- `subscribe`: Allows you to listen for state changes in the Store.

The Store ensures that state is kept consistent across your application.

### Action

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

Reducers are pure functions that take the current state and an action, and return a new state. They describe how the state changes in response to an action. Reducers should be deterministic, meaning given the same input, they should always return the same output.

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

