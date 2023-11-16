
## Introduction
This tutorial will provide a begginer friendly instruction to master React useEffect Hook and its application in software development. There will also be some real world examples demonstrating its power of api call execution. Specifically, we will be using the Axios, one of the most popular javascript Promise-based library for sending http request.

## What is “useEffect”?
In React.js, the functional components generally serve the purpose of rendering and displaying contents on the webpage. However, how are things such as asychronous API data fetching or conditionally updating the elements at any time (typically called “side effects” in most online resources) handled? The solution is “useEffect Hook”, an essential hook that frontend developers use to communicate with database or DOM. 

## Understand UseEffect Hook Syntax

On top of the file in an React application:
```jsx
import { useEffect } from ‘react’;
```

``` jsx
function MyReactComponent() {
    // the function that creates the "side effect"
    useEffect(function() {
        // define your side effects here.
        console.log("I can perform side effects.")
        return function() {
            // clean up the effects for performance optimization
            console.log("I am the clean up function.")
        }
    }, []); //Dependency Array

    return (<div>Hello</div>);
}
```
You can also pass in an arrow function as first argument as following:
```jsx
function MyReactComponent() {
    useEffect(() => {
        console.log("I can perform side effects.")
        // Smilarly the cleanup function could also be returned as arrow function.
        return () => {
            console.log("I am the clean up function.")
        }
    }, []); //Dependency Array

    return (<div>Hello</div>);
}
```

UseEffect Hook must be used inside a react component and it takes in two arguments:
1.	A function that handles the “side effects” and returns a cleanup function.
2.	An optional dependency array that determines when the function would be triggered. 