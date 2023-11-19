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
I will list the key parts of state for NgRx state management. With each part of state I will give an example with a simple "User" object being added to state. 
1. Store: The central piece of NgRx is the store, which holds the entire state of the application. It is a single immutable data structure.
``` javascript
// app.state.ts
export interface AppState {
  user: User;
}

// user.model.ts
export interface User {
  id: number;
  username: string;
}
```
2. Actions: Actions are plain JavaScript objects that describe unique events in the application. They are used to trigger changes to the state.
``` javascript
// user.actions.ts
import { createAction, props } from '@ngrx/store';

export const setUser = createAction('[User] Set User', props<{ user: User }>());
export const clearUser = createAction('[User] Clear User');
```
3. Reducers: Reducers are pure functions that take the current state and an action, and return a new state. They define how the state changes in response to actions.
``` javascript
// user.reducer.ts
import { createReducer, on } from '@ngrx/store';
import * as UserActions from './user.actions';

export const initialState: User = { id: 0, username: '' };

export const userReducer = createReducer(
  initialState,
  on(UserActions.setUser, (state, { user }) => user),
  on(UserActions.clearUser, () => initialState)
);
```
4. Selectors: Selectors are functions that retrieve slices of the state. They help in obtaining specific pieces of information from the application state.
``` javascript
// user.selectors.ts
import { createSelector, createFeatureSelector } from '@ngrx/store';
import { AppState } from './app.state';

export const selectUserState = createFeatureSelector<AppState, User>('user');

export const selectUserId = createSelector(
  selectUserState,
  (state) => state.id
);

export const selectUsername = createSelector(
  selectUserState,
  (state) => state.username
);
```
5. Effects: Effects are used to manage side effects in your application, such as asynchronous operations. They listen for actions and perform additional logic. Often times this is where your API calls are made. This is the best technique for separating backend interaction logic from pure frontend rendering logic. 
``` javascript
// user.effects.ts
import { Injectable } from '@angular/core';
import { Actions, ofType, createEffect } from '@ngrx/effects';
import { mergeMap, map } from 'rxjs/operators';
import * as UserActions from './user.actions';
import { UserService } from './user.service';

@Injectable()
export class UserEffects {
  loadUser$ = createEffect(() =>
    this.actions$.pipe(
      ofType(UserActions.loadUser),
      mergeMap(() =>
        this.userService.getUser().pipe(
          map((user) => UserActions.setUser({ user }))
        )
      )
    )
  );

  constructor(private actions$: Actions, private userService: UserService) {}
}
```
# NgRx Memoization for Expensive Calls to State
We can use the same form of memoization we learned in our algorithm classes and apply it to state! Memoization involves caching the results of expensive function calls and returning the cached result when the same inputs occur again. This can be applied to selectors in NgRx to prevent unnecessary recomputation. An example of memoization following the "User" state is shown below:
``` Javascript
// Before memoization
export const selectUserById = (state: AppState, userId: number) => state.users.find(user => user.id === userId);

// After memoization
import { createSelector } from '@ngrx/store';

export const selectUserById = createSelector(
  selectAllUsers,
  (users, props) => users.find(user => user.id === props.userId)
);
```

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