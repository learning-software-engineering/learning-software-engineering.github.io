# Intro to Reactstrap, a React Library for Bootstrap

## Table of contents
### [Introduction](#preface)
### [What is Reactstrap](#what-is-reactstrap)
### [Where to begin](#where-to-begin)
### [Reactstrap Basics](#reactstrap-basics)
### [Conclusion](#conclusion)

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

<img alt="image" src="https://i.ibb.co/ft8WHq9/Screenshot-2023-11-29-at-8-58-16-PM.png" width="400" height="300">

As you can see, the colour "primary" corresponds to the blue colouring of the button shown in the image. There are many other colour names built in to Reactstrap. Here is a link to the [Reactstrap Button documentation](https://reactstrap.github.io/?path=/docs/components-button--button), which contains more information about styles and colours for the Button component.

In addition to Button, Reactstrap offers a large library of components. Here is a list of some of the most popular, with links to their documentation:
- [Card](https://reactstrap.github.io/?path=/docs/components-card--card)
- [Carousel](https://reactstrap.github.io/?path=/docs/components-card--card)
- [Forms](https://reactstrap.github.io/?path=/docs/components-forms--input)
- [Nav](https://reactstrap.github.io/?path=/docs/components-nav--navs)
- [Modal](https://reactstrap.github.io/?path=/docs/components-modal--modal)
- [Table](https://reactstrap.github.io/?path=/docs/components-table--table)
- [Pagination](https://reactstrap.github.io/?path=/docs/components-pagination--pagination)

And many more can be found on the Reactstrap website [linked here](https://reactstrap.github.io/).

## Conclusion
You should now be familiar with the purpose of the Reactstrap library. It is a great way to easily create styled React components without having to design your own custom CSS classes. We went over the steps for installing and setting up Reactstrap for usage in your React projects, as well as an example of how we apply it in the code. Now that you have an idea of the basics, I encourage you to create your own stylish React components using the Reactstrap library, and to follow the links to the documentation to take your Reactstrap development to a new level!
