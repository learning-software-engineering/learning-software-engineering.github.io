# Angular

## Table of contents
### [Introduction](#introduction-1)
### [Resources](#resources-1)

## Introduction
Angular is a framework which allows people to create responsive single page web apps. It is built on TypeScript and can be used to build scalable web apps, has a collection of well-integrated libraries which cover many features and several tools to help build, test and maintain your code. With Angular you can create single-page-application where you have a single html file where changes are rendered in the browser. Familiarity with HTML/CSS as well as JavaScript/TypeScript will be needed while building your web app.

## NgRx State Management
Angular applications often deal with complex state management as they grow in size and complexity. NgRx is a well-organized state management library for Angular applications that leverages reactive programming concepts. It is inspired by Redux, a popular state management library for React applications, but is more structured (in file structure and component interaction). 

# Install NgRx
You can get started with NgRx by using this npm command: 
```bash 
npm install @ngrx/store @ngrx/effects @ngrx/store-devtools. 
```

# Key Parts of State
1. Store: The central piece of NgRx is the store, which holds the entire state of the application. It is a single immutable data structure.
2. Actions: Actions are plain JavaScript objects that describe unique events in the application. They are used to trigger changes to the state.
3. Reducers: Reducers are pure functions that take the current state and an action, and return a new state. They define how the state changes in response to actions.
4. Selectors: Selectors are functions that retrieve slices of the state. They help in obtaining specific pieces of information from the application state.
5. Effects: Effects are used to manage side effects in your application, such as asynchronous operations. They listen for actions and perform additional logic. Often times this is where your API calls are made. This is the best technique for separating backend interaction logic from pure frontend rendering logic. 

# NgRx Benefits
1. Predictable State Management: NgRx provides a clear and predictable way to manage the state of your application.
2. Debugging: With the DevTools extension, you can track state changes and actions, making it easier to debug your application.
3. Scalability: NgRx scales well as your application grows, providing a structured approach to state management.
4. Reactive Programming: NgRx leverages reactive programming principles, making it easier to handle asynchronous operations.

# NgRx Difficulties
1. Size: NgRx requires an expansive file structure (ideally one file for each part of state for each component). For smaller projects this will not be ideal.
2. Boilerplate Code: This becomes less of a problem as more components have been implemented in state, but much of NgRx state is boilerplate code which must be implemented in each file respectively.

## Additional Resources
Official Angular documentation can be found here. \
https://angular.io/docs

Sololearn offers a free Angular course. \
https://www.sololearn.com/learning/1092

udemy also offers a deeper and more comprehensive Angular course although you do have to pay for it. \
https://www.udemy.com/course/the-complete-guide-to-angular-2/

stackblitz is a great way to test your code online for free with your github account. \
https://stackblitz.com/

Angular also has its own set of official sources which can be found here. \
https://angular.io/resources?category=community