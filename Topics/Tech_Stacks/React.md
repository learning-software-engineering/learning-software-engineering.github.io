## Tech Stacks

### React Overview
React is a Javascript library used to build user interfaces. As such, you're going to have to know HTML, CSS and Javascript in order to learn React.
It's ease of use and popularity comes from how little you actually have to code. Easily applicable for any frontend interface, if you're going to use any library/framework for frontend development, React is the safest option.

### How to Start a React Project

First of all, make sure Node.js is installed in your computer. If not, you can download it from this [link](https://nodejs.org/en/download) and follow the instructions to install.

You can check whether the installment was succesful by running:
```
node -v
```

Make sure `npm` is also installed properly by running:
```
npm install npm --global
```

Now, go to the folder that you wish to create your React project in. Then, run the following command:
```
npx create-react-app my-first-app
```

Congrats! The `npm` will handle the necessary files for the skeleton of your React project and initiate template files for you to start working with. You can see the current app build by going into the app folder with the `cd` command and running:
```
npm start
```

This command will host your React frontend appliation on `localhost:3000` by default and open a browser tab for this address.

![Browser view of the initial React app build](https://www.freecodecamp.org/news/content/images/2021/03/Screen-Shot-2021-02-03-at-8.56.40-PM.png)

React framework handles frontend designs as functional components stacked together. As a design principle, developers usually start by creating small and reusable components like navbars or buttons. Then, they use these components inside other larger components to build the whole website with a bottom-up approach.

### Useful Libraries

**1) Formik:** Formik is a library to create and maintain HTML forms in React apps in a very concise manner. It enables users to easily update values, enforce validation constraints and handle submission events in a few lines. \
Install it by running:
```
npm install formik --save
```


Click [here](https://www.youtube.com/watch?v=vJtyp1YmOpc) for a useful video guide on Formik.

**2) Styled Components:** Styled components is a library to integrate CSS designs into React components. It enables developers to write their CSS code directly into JavaScript files in their React project and wrap it up as another component. This method allows a more compact styling implementation as well as providing an easy variable passing technique into CSS designs. \
Install it by running:
```
npm install --save styled-components
```
Example:
```
import styled from 'styled-components';
import { height, color, space } from 'theme';

const StyledButton = styled.button`
    height: ${height('button')}px;
    padding: 0 ${space(2)};
    border: 0;
    background-color: ${color('primary')};
    color: ${color('white')};
`;
```
compiles into
```
button {
    height: 40px;
    padding: 0 16px;
    border: 0;
    background-color: #3b49df;
    color: #ffffff;
}
```
Click [here](https://www.youtube.com/watch?v=-FZzPHSLauc) for a useful video guide on Styled Components.

### React Resources 

These frontend challenges for HTML, CSS and JavaScript will help you review core skills while also making interesting projects as well. \
https://www.frontendmentor.io/


Basic React tutorial provided by the official React website. This tutorial will guide you through a very basic tutorial that you can do straight from your browser. \
https://reactjs.org/tutorial/tutorial.html


React tutorial by MDN Web Docs. Useful readings for if you have time, but not necessary by any means.\
https://developer.mozilla.org/en-US/docs/Learn/Tools_and_testing/Client-side_JavaScript_frameworks/React_getting_started


Javascript frameworks tutorial provided by Microsoft. Useful readings, but not necessary to learn React. \
https://learn.microsoft.com/en-us/windows/dev-environment/javascript/


1 hour in depth tutorials about React. These Youtube crash course provides a great in depth look at React and the various important components that you will be using most often. Very useful if you are learning React under a strict time limit for whatever reason. \
https://www.youtube.com/watch?v=w7ejDZ8SWv8 \
https://www.youtube.com/watch?v=b9eMGE7QtTk 


Online development environment to try React out in (Among other frontend tools). Great for testing the waters with React to see if it will be something you want to learn or not. \
https://codepen.io/


Host your React websites straight from your Github repo. Website hosting is fairly expensive, so this is here as a free alternative for website deployment. \
https://pages.github.com/
