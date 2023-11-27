# Learning TypeScript

## Table of contents
### [Introduction](#introduction-1)
### [Why use TypeScript](#why-use-typescript-1)
### [How to use TypeScript](#how-to-use-typescript-1)
### [Additional Resources](#additional-resources-1)


## Introduction

TypeScript is a programming language that extends JavaScript's capabilities by including optional static type checking and other features. TypeScript is a superset of JavaScript. In other words, TypeScript adds new features on top of the existing JavaScript language, such as optional static typing, classes, interfaces, and more, while still maintaining compatibility with the existing JavaScript ecosystem.

If you aren't that familiar with JavaScript, you can learn about JavaScript and TypeScript and their relationship [here](https://www.typescriptlang.org/docs/handbook/typescript-from-scratch.html).

If you are already familiar with JavaScript, you can learn more about TypeScript and see some examples [here](https://www.typescriptlang.org/docs/handbook/typescript-in-5-minutes.html).

To play around with and experiment using TypeScript, feel free to visit the [playground page](https://www.typescriptlang.org/play).

## Why use TypeScript

TypeScript allows developers to catch potential errors early in the development process (at compile-time instead of runtime) and write more maintainable and scalable code. This can greatly reduce the likelihood of bugs and make code more reliable and easier to maintain, as well as improve code readability and make it easier to write reusable code. This makes TypeScript the preferred choice when building large-scale applications, especially in web development. Its syntax is similar to JavaScript, making it easy to learn and adopt for developers familiar with JavaScript. Additionally, popular code editors such as VSCode offer additional quality-of-life functionalities such as autocompletion when writing in TypeScript, making it easier and faster to write code.

To learn more about why you should consider using TypeScript over JavaScript, visit [this blog here](https://www.geeksforgeeks.org/8-reasons-why-you-should-pick-typescript-over-javascript/).

## How to use TypeScript

You can integrate TypeScript into any JavaScript code, but it is most commonly used for web development using JavaScript frameworks such as React and Angular.

Here is how to create projects with the above frameworks using TypeScript.

### React

You can find the complete guide [here](https://create-react-app.dev/docs/adding-typescript/). To learn more about React and TypeScript, you can also follow [this YouTube video by Ben Awad](https://www.youtube.com/watch?v=Z5iWr6Srsj8&t=28s&ab_channel=BenAwad).

To create a React project with TypeScript enabled, follow these basic steps:

1. Make sure you have Node.js installed on your machine. If you don't have Node.js installed, you can visit the official Node.js page [here](https://nodejs.org/en) and follow the installation steps.
2. Open a terminal and navigate to the directory where you want to create your app.
3. Run the following command to create a new React app with TypeScript:

    `npx create-react-app my-app --template typescript`

That's it! Now you can use TypeScript files in your React project!

### Angular

Angular comes with TypeScript enabled by default. In fact, Angular is built entirely in TypeScript, and is the recommended language for developing Angular applications. This is a summary of the guide found [here](https://angular.io/guide/setup-local). To learn more about Angular and TypeScript, you can watch [this in-depth YouTube course by Mosh](https://www.youtube.com/watch?v=k5E2AVpwsko&t=1692s&ab_channel=ProgrammingwithMosh).

1. Make sure you have Node.js installed on your machine. If you don't have Node.js installed, you can visit the official Node.js page [here](https://nodejs.org/en) and follow the installation steps.

2. Open a terminal and install the Angular CLI by using the following command

    `npm install -g @angular/cli`
3. Open a terminal and navigate to the directory where you want to create your app.
4. Run the following command to create a new workspace and initial starter app:

    `ng new my-app`'

### Vue

To use TypeScript in your Vue 3 project using `create-vue`, which is the official Vue project scaffolding tool, follow the steps below:

1. Open a terminal window, navigate to the location where the project will be created. 

2. Run the command `npm create vue@latest` to initiate the project creation. (Note: if you do not have Node.js installed on your machine, follow the guide in the sections above to install it first before creating the Vue project)

3. Follow the command line prompts to select the preferences for your project. Select `yes` for the prompt `Add TypeScript?`, and manage other settings to your preference.

4. Done! The Vue project is succesfully created.

It is worth noting that this method is the preferred way to create Vue projects, instead of using Vue CLI, since create-vue is based on Vite. For more information, visit the create-vue Github repository [here](github.com/vuejs/create-vue).
For a more detailed overview of using TypeScript with Vue, visit the [official Vue.js guide page](vuejs.org/guide/typescript/overview.html).

## Additional Resources

- If you are interested, you can take a look at [this free course by codecademy on TypeScript](https://www.codecademy.com/learn/learn-typescript).
- [This guide by freecodecamp](https://www.freecodecamp.org/news/learn-typescript-beginners-guide/) is another great resource for learning how to use TypeScript.
- To learn more about TypeScript features in depth, you can watch [this YouTube playlist by The Net Ninja](https://www.youtube.com/playlist?list=PL4cUxeGkcC9gUgr39Q_yD6v-bSyMwKPUI)