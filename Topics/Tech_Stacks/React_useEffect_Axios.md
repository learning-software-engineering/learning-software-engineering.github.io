# Learning UseEffect Hook with Axios

## Table of Contents
### [Introduction](Introduction-1)
### [What is useEffect Hook?](What-is-UseEffect-Hook?-1)
### [Understand useEffect Hook Syntax](Understand-useEffect-Hook-Syntax-1)
### [What is Dependency Array?](What-is-Dependency-Array?-1)
### [useEffect Hook Application with Axios](useEffect-Hook-Application-with-Axios-1)
### [Additional Resources](Additional-Resources-1)

## Introduction
This tutorial will provide a begginer friendly instruction to master React useEffect Hook and its application in software development. There will also be some real world examples demonstrating its power of api call execution. Specifically, we will be using the Axios, one of the most popular javascript Promise-based library for sending http request.

## What is useEffect Hook?
In React.js, the functional components generally serve the purpose of rendering and displaying contents on the webpage. However, how are things such as asychronous API data fetching or conditionally updating the elements at any time (typically called “side effects” in most online resources) handled? The solution is “useEffect Hook”, an essential hook that frontend developers use to communicate with database or DOM. 

## Understand useEffect Hook Syntax

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

## What is Dependency Array?
There are three major cases:
##### Case 1: Non-Empty Dependency Array
 By default, useEffect would fire when the component mounts. And after that, the useEffect would run whenever there is a state change in any of the variables in the dependency array. This is particularly useful in software engineering when you want to implement a search functionality, such that after user enter the input or apply some filter, a get request would be made to the server and update the data in real time. 

##### Case 2: Empty Dependency Array
Since nothing is provided inside the dependency array, the effect function would only be called once upon initial mount. Compare with case 1, this property renders its exceptional value when you want to load data only "once" when the user opens or refreshes the web page. For instance, we can use it when we are asked to create an attendence report of the workers. We obviously want it to only make one GET request instead of an infinite loop of requests that fires every second.

##### Case 3: No Dependency Array as Argument 
Since there is no dependency array at all,  it means that the useEffect function would run everytime ```<MyReactComponent/>``` rerenders. This flavor of useEffect Hook is not commonly used compared to the other two due to its limitation. For instance, when the side effect includes some data fetching instead of the console.log, the drawback would become obvious. Since every time the components is re-rendered, there would be a request sent to the server, which could easily cause some performance issue. 

## useEffect Hook Application with Axios

```jsx
import axios from "axios";
import { useEffect, useState } from "react";

function ActivityDisplay() {
    const [data, setData] = useState(null);
    const [isLoading, setIsLoading] = useState(true);
    const [errorMsg, setErrorMsg] = useState(null)
    useEffect(() => {
        async function fetchRandomActivity() {
            setErrorMsg(null);
            setIsLoading(true);

            await axios.get("http://www.boredapi.com/api/activity")
            .then((resp)=> {
                setData(resp.data); 
            })
            .catch((e) => {
                console.log(e); 
                setErrorMsg(e);
            })
            .finally(() => {
                setIsLoading(false);
            })
        }
      fetchRandomActivity();
      }, []);

    return (
        <div>
            {isLoading? <h1>Loading...</h1>: (data && <p>{data.activity}</p>)}
            {errorMsg && <h1>{errorMsg.message}</h1>}
        </div>
    )
}

export default ActivityDisplay;
```
The code above is a simplified example to help you understand the proper way of making Http request to the server through useEffect Hook. Notice that we first declared three states: 1\) ```data``` obviously store the data in the http response after calling axios.get. 2\) ```isLoading``` signifies the data fetching is not yet complete. 3\) ```errorMsg``` stores the potential error during the fetching process.

 The latter two are typically used for better UX, since data fetching sometimes would lead to some delays if you are trying to query a real-world database. Conditionlly rendering a loader would notify user that the webpage is still in the process of fetching the intended contents as opposed to a webpage freeze. 
 
 In the catch block appropriate error handling could also speed up the debugging process. 

 In the useEffect Hook, we can observe that the dependency array does not contain any state since the client side only need to make the GET request once. That means we only want ```<ActivityDisplay/>``` to fetch and load the content on mount. 

#### Conclusion
 After this tutorial, hope you have a basic understanding of useEffect Hook as well as its application in data fetching using Axios. Here are some additional links if you would like to explore more about useEffect Hook.

## Additional Resources
The offical documentation for useEffect Hook:

https://react.dev/reference/react/useEffect

A blog post that goes into depth about the cleanup function:

https://blog.logrocket.com/understanding-react-useeffect-cleanup-function/

FreeCodeCamp Tutorial about Axios in React:

https://www.freecodecamp.org/news/how-to-use-axios-with-react/
 