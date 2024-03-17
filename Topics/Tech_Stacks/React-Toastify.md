# React Toastify Guide

React Toastify stands as a widely favored library for crafting toast notifications within React applications.

This tool simplifies the process of generating responsive toast notifications, which are pop-up messages that relay information such as success, errors, loading statuses, or warnings, typically appearing on the edge of the screen. Optionally, these notifications can feature progress bars to indicate ongoing processes. A diverse array of toast notification styles is available.\

## Table of Contents
1. [Installation](#installation)
2. [Creating a Basic Toast Notification](#creating-a-basic-toast-notification)
3. [Types of Toast Notifications](#types-of-toast-notifications)
4. [Toast Notification Placement](#toast-notification-placement)
5. [Useful Customization](#useful-customization)
    - [Handling Auto Close](#handling-auto-close)
    - [Limit the Number of Toasts Displayed](#limit-the-number-of-toast-displayed)
    - [Implementing a Controlled Progress Bar](#implementing-a-controlled-progress-bar)
    - [Updating a Toast When an Event Happens](#updating-a-toast-when-an-event-happens)
6. [Useful Customization](#useful-customization)
7. [References](#references)



## Installation
React Toastify can be added into your project with a few simple commands. Ensure you have a React environment ready, either by adding to an existing project or starting fresh with `create-react-app`.

To add React Toastify to your project, execute the following:

```bash
npm install --save react-toastify
```

Or, if you prefer yarn:
```bash
yarn add react-toastify
```

## Creating a Basic Toast Notification
The initiation of a basic toast notification is quite simple. In your main JavaScript file, typically `App.js`, start by importing React Toastify and its accompanying styles:

```javascript
import { ToastContainer, toast } from 'react-toastify';
import 'react-toastify/dist/ReactToastify.css';
```

Next, you can create a function that triggers the toast:
```javascript
function App(){
  const notify = () => toast("This is a toast notification !");
  return (
    <div>
      <button onClick={notify}>Notify !</button>
      <ToastContainer />
    </div>
  );
}

```
## Creating a Promise Toast Notification
In React, a toast promise refers to a promise mechanism that facilitates the execution of code asynchronously. This enables the initiation of certain actions or events when a toast notification is shown. For instance, it could lead to the redirection of the user to another webpage or the exhibition of an alert message, with all errors being adequately managed.

```javascript
import React, { useEffect } from "react";
import { ToastContainer, toast } from 'react-toastify';
import 'react-toastify/dist/ReactToastify.css';

function App() {
  // Define the data fetching operation as a function that returns a promise
  const fetchData = () => {
    return new Promise((resolve, reject) => {
      fetch("https://test123.com/api/")
        .then(response => response.json())
        .then(data => setTimeout(() => resolve(data), 5000)) // Simulate a delay
        .catch(error => reject(error));
    });
  };

  useEffect(() => {
    // Use toast.promise to handle the promise returned by fetchData
    toast.promise(
      fetchData(), // Execute the fetchData function
      {
        pending: 'logging in ...', 
        success: "Welcome user",
        error: "Error logging in"
      }
    );
  }, []);

  return (
    <>
      <ToastContainer />
    </>
  )
}

export default App;
```
![image06-ezgif com-crop](https://github.com/learning-software-engineering/learning-software-engineering.github.io/assets/69292669/dbd448ab-48c4-49cb-b0ed-d1e022dbee1d)





## Types of Toast Notifications

React Toastify provides five distinct types of toast notifications, each for different scenarios. Here’s how to initiate each:
1. Default
  ```javascript
  const notify = () => toast("This is a toast notification !");
  ```
![default-notification](https://github.com/learning-software-engineering/learning-software-engineering.github.io/assets/69292669/3329a833-d0ad-4136-b2ff-65bde8f3b9e4)

2. Info
  ```javascript
   const notify = () => toast.info("This is an info toast notification !");
   ```
![toast-info-notification](https://github.com/learning-software-engineering/learning-software-engineering.github.io/assets/69292669/92b86889-879b-4cc1-8fa6-e222d3e87c45)

3. Success
  ```javascript
   const notify = () => toast.success("This is a success toast notification !");
   ```
![success-toastofy-notification](https://github.com/learning-software-engineering/learning-software-engineering.github.io/assets/69292669/719676bf-dd27-4ebb-9d51-63b8806f0521)

4. Warning
  ```javascript
   const notify = () => toast.warning("This is a warning toast notification !");
   ```
![toast-warning-notification](https://github.com/learning-software-engineering/learning-software-engineering.github.io/assets/69292669/b090d7e2-1bd7-467d-a1a6-930ca708d7fc)

5. Error
  ```javascript
   const notify = () => toast.error("This is an error toast notification !");
   ```
![error-toast-notification](https://github.com/learning-software-engineering/learning-software-engineering.github.io/assets/69292669/ab0d49b3-dc6e-4e0d-90bc-2751f695d602)

You can use these notifications by including them in a function like so:
  ```javascript
   function Toastify(){
    const notify = () => toast.error("This is a toast notification !");
    return (
      <div>
        <button onClick={notify}>Notify !</button>
        <ToastContainer />
      </div>
    );
  }
```
Replace toast.error with any of the other types as needed.


## Toast Notification Placement
React Toastify allows for the customization of the toast's display location. Here are the options:

the available positions are:
```javascript
<ToastContainer position="top-left" />
<ToastContainer position="top-right" />
<ToastContainer position="top-center" />
<ToastContainer position="bottom-left" />
<ToastContainer position="bottom-right" />
<ToastContainer position="bottom-center" />
```


# Useful Customization 
Here are few customization that I find it handy in most application:

## Handling Auto Close
The autoClose property accepts a time in milliseconds, dictating how long the toast will stay visible:

```javascript
import { ToastContainer, toast } from 'react-toastify';

<ToastContainer autoClose={3000} />

```
You can  prevent the toast notification from closing by default using the false statement instead of the seconds like:
```javascript
toast("This toast won't close automatically", { autoClose: false });

```

You can also individually close each toast at different points in time:

```javascript
function ToastController(){
  const quickToast = () => toast("closeAfter2Seconds", { autoClose: 2000 });
  const slowToast = () => toast("closeAfter10Seconds", { autoClose: 10000 });

  return (
    <div>
      <button onClick={quickToast}>Quick Toast</button>
      <button onClick={slowToast}>Slow Toast</button>
      <ToastContainer />
    </div>
  );
}


```
![individually-close-toast-notification](https://github.com/learning-software-engineering/learning-software-engineering.github.io/assets/69292669/724d14e8-7ef1-4dbe-b287-bb6afff8c4b6)


## Limit the number of toast displayed
Control the number of toasts displayed simultaneously with the limit property:

```javascript
import React from 'react';
import { toast, ToastContainer } from 'react-toastify';
import 'react-toastify/dist/ReactToastify.css';

function ToastLimiter(){
  const makeToast = () => {
    toast("A toast message");
  }

  return (
    <div>
      <button onClick={makeToast}>Generate Toast</button>
      <ToastContainer limit={3} />
    </div>
  );
}
```
When the limit is reached, additional toasts join a queue and appear as others close.

Clear the queue with:
```javascript
toast.clearWaitingQueue();

```


## Implementing a controlled progress bar
For operations like file uploads, a controlled progress bar can be beneficial:
```javascript
import React from 'react';
import axios from 'axios';
import { toast } from 'react-toastify';

function UploadProgress(){
  const toastId = React.useRef(null);

  function beginUpload(){
    // Simulate file upload
    setTimeout(() => {
      if (toastId.current === null) {
        toastId.current = toast('Uploading...', { progress: 0 });
      }

      // Simulate progress
      toast.update(toastId.current, { progress: 0

```


## Updating a toast when an event happens
Toast notifications in React can be dynamically updated in response to various events, such as the completion of a file upload to a server. Here are a few ways you can modify an active toast notification:

1. Adjust the Toast Type or Visual Style:
You can alter the appearance or type of a toast using the update method.
```javascript
import React, { useRef } from 'react';
import { toast } from 'react-toastify';

function InteractiveToast() {
  const toastRef = useRef(null);

  const launchToast = () => {
    toastRef.current = toast("Wait for it...", { autoClose: false });
  };

  const transformToast = () => {
    toast.update(toastRef.current, { type: toast.TYPE.SUCCESS, autoClose: 5000 });
  };

  return (
    <div>
      <button onClick={launchToast}>Show Toast</button>
      <button onClick={transformToast}>Transform Toast</button>
    </div>
  );
}

```

2. Change the content of the toast
The content of a toast can be updated to a simple string, a React component, or any valid JSX.
 ```javascript
 // Change to a simple string
toast.update(toastId, {
  render: "Content updated!",
  type: toast.TYPE.DEFAULT,
  autoClose: 5000
});

// Change to a React component
toast.update(toastId, {
  render: <CustomComponent />,
  type: toast.TYPE.DEFAULT,
  autoClose: 5000
});

// Change using JSX
toast.update(toastId, {
  render: <div>Brand new content here</div>,
  type: toast.TYPE.DEFAULT,
  autoClose: 5000
});

```
3. Apply a transition when the change happens
Transitions can add a polished effect to your toast updates, enhancing the user experience.
```javascript
toast.update(toastId, {
  render: "Updated with a transition!",
  type: toast.TYPE.DEFAULT,
  transition: Slide
})
```

## References

Here are some useful resources for further reading and advanced concepts in React Toastify:

- [React Toastify: The Complete Guide](https://deadsimplechat.com/blog/react-toastify-the-complete-guide/#limit-the-number-of-toast-displayed) - An extensive guide covering the gamut from basic to advanced usage of React Toastify, including limiting the number of displayed toasts.
- [React Toastify Official Documentation](https://fkhadra.github.io/react-toastify/introduction/) - The official documentation provides in-depth information about all the features that React Toastify offers, including installation, API references, and examples.
