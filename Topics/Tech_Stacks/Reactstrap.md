# Intro to Reactstrap, a React Library for Bootstrap

## Table of contents
### [Introduction](#what-is-reactstrap?-1)
### [What is Reactstrap](#what-is-reactstrap?-1)
### [Where to begin](#where-to-begin-1)
### [Reactstrap Basics](#reactstrap-basics-1)

## Preface
This will serve as a guide for the basics of incorporating Reactstrap into your React frontend development. After reading, you will know how to install and setup the Reactstrap library for use in your React project. You will also be introduced to some popular Reactstrap components, and gain an understanding of the benefits of incorporating Reactstrap into your web app development. Prior knowledge of React and Bootstrap is recommended. The more familiar you become with React, the easier it becomes to incorporate Reactstrap into your workflow. Experience with Bootstrap will allow you to quickly adapt to using Reactstrap. Familiarity with CSS is also recommended as this allows you to understand what Reactstrap provides at a lower-level, which will allow you to further appreciate the advantages of incorporating Reactstrap into your workflow.
## What is Reactstrap?
Reactstrap is a React component library for Bootstrap. This means that Reactstrap provides a collection of pre-built React components designed to work seamlessly with the Bootstrap framework (Which is typically used within an HTML/CSS setup). Reactstrap simplifies the process of using Bootstrap's styles and components within a React application. This makes for a convenient integration of Bootstrap into React-based projects.
## Where to begin
We will assume you have an existing React project already created. If this is not the case, you can refer to the React documentation for the steps in creating a React project [here](https://react.dev/learn/start-a-new-react-project). Once you have your React project ready to go, we can set up Reactstrap. We will start by installing the necessary packages. First you will need to install Bootstrap using this command: 

```
npm install --save bootstrap
```
Then we will install the actual Reactstrap library using the following command:

```
npm install reactstrap react react-dom
```

You will also want to import Bootstrap CSS into your src/index.js file in order for Reactstrap to have access to Bootstrap styles:

```
import 'bootstrap/dist/css/bootstrap.css';
```
After these steps are complete, you are ready to begin using Reactstrap for styling within your React components.
## Reactstrap Basics
To get started using Reactstrap, navigate to the desired React component within your project. Now import the required Reactstrap components at the top of this component file like so:
```
import { Button } from 'reactstrap';
```
Here we have used the "Button" component as an example import. You can import any components you require for your specific use-case, and you can import them within the same import statement by separating each of their names with commas. Here is the code for the file of a React component with example usage of the Button component:
```
// MyButtonComponent.js

import React from 'react';
import { Button } from 'reactstrap';

const MyButtonComponent = () => {
  return (
    <div>
      <h1>Hello, Reactstrap Button!</h1>

      {/* Example of using Reactstrap Button component */}
      <Button color="primary">
        Click me
      </Button>
    </div>
  );
};

export default MyButtonComponent;
```
In this file, we have simply created a button with the words "Click me" written on it. The button does not perform any functionality, feel free to experiment and add your own!
Here is what this file looks like when it is ran locally (using npm start):
<img alt="image" src="https://i.ibb.co/ft8WHq9/Screenshot-2023-11-29-at-8-58-16-PM.png" width="300" height="200">


Reactstrap offers a large library of componenets. Here is a list of some of the most popular, with links to their documentation:
- Button
- 
