# An introduction to Chakra UI

## Introduction
Chakra UI is a UI component library specifically designed for React. It provides a comprehensive set of pre-styled components ranging from basic layout components to advanced form inputs, modals, loading bars, and way more. Chakra UI has a powerful and React-forward prop-based styling system that easily allows for responsive design as well as a high degree of customizability.

## Installation & Setup
### Installation
To install Chakra UI you can use the Node Package Manager (npm) or yarn:
```bash
npm install @chakra-ui/react @emotion/react @emotion/styled framer-motion
# or
yarn add @chakra-ui/react @emotion/react @emotion/styled framer-motion
```
### Setup
Once Chakra UI has been installed to your React app, your application will need to become a child of the `ChakraProvider` to begin utilizing Chakra's pre-styled components. Your `App.jsx` should look roughly similar to this snippet from [Chakra UI's website](https://chakra-ui.com/getting-started):
```js
import * as React from 'react'

// 1. import `ChakraProvider` component
import { ChakraProvider } from '@chakra-ui/react'

function App() {
  // 2. Wrap ChakraProvider at the root of your app
  return (
    <ChakraProvider>
      <TheRestOfYourApplication />
    </ChakraProvider>
  )
}
```

## Usage

### Design principles

Chakra UI employs several key design principles:

- **Prop-based styling**: a component's style can be customized by passing in a prop corresponding to a CSS property.
- **Responsive-forward design**: responsive design is both easy to implement and highly customizable as a result of Chakra UI's seamless integration of media queries and breakpoints to custom styling
- **Dark mode**: custom styling for both light and dark modes is closely integrated into Chakra UI's styling system

### Using UI components



### Styling components

A component's style can be customized by passing certain props to it. The props that are accepted rougly correspond to CSS properties, and accept any value that CSS accepts.

For example, the following creates a box with styling that corresponds to the CSS property `margin-left: 10px;`
```jsx
<Box marginLeft={'10px'}></Box>
```
To make development faster and reduce code clutter, many commonly used props also have abbreviated aliases that are shorter and more legible. For example, in the above example, `ml` is the abbreviated alias of `marginLeft`, so it would be equivalent to:
```jsx
<Box ml={'10px'}></Box>
```
A list of props, their aliases, as well as their corresponding CSS class can be found [here](https://chakra-ui.com/docs/styled-system/style-props).

Pseudo classes also exist in this styled prop system. Pseudo classes are differentiated with an underscore at the beginning of the prop and they accept an object of prop name and value key-value pairs. For example, the following created a box which changes the background to red when hovered over:
```jsx
<Box _hover={{ bg: 'red' }}></Box>
```
Other common pseudo classes would include `_active`, `_focus`, `_before`, etc. A full list of pseudo classes can be found [here](https://chakra-ui.com/docs/styled-system/style-props#pseudo)

### Responsiveness

 

### Theming



## Benefits and Drawbacks

### Benefits
- **Accessibility**: Chakra UI prioritizes accessibility, ensuring that components are usable by everyone, including those with disabilities.
- **Easy to Build Complex Interfaces**: Chakra UI's component-based architecture follows a modular approach, meaning complex interfaces can be easily created through composing smaller, reusable components.
- **Intuitive Documentation***: The developer experience of Chakra UI is strong through Chakra UI's intuitive and clear [documentation](https://chakra-ui.com/docs/styled-system/style-props). This means, important explanations, for concepts such as responsive design and styling, can always be easily understood and found.
- **Performance**: Chakra UI was built with performance in mind, utilizing optimization techniques that are often too cumbersome or difficult to implement when using plain CSS and JS in a personal project.

### Drawbacks
- **Learning Curve**: Even though Chakra UI strongly focuses on simplifying the front end development process, component libraries can always feature a learning curve to beginners who are unfamiliar with the workflow surrounding component-based architecture
- **Bundle Size**: Including Chakra UI in a project often increases the bundle size, increasing the cumbersome nature of a build.
- **Design Consistency**: Due to Chakra UI's increased styling complexity over more traditional non-React CSS component libraries, maintaining design consistency across a project with multiple team members will require coordination and communication over styling decisions.


## Resources
- [Chakra UI](https://chakra-ui.com/)
- [Chakra UI's NPM Page](https://www.npmjs.com/package/@chakra-ui/react)
- [Informative Chakra UI Tutorial Video Series](https://www.youtube.com/watch?v=iXsM6NkEmFc&list=PL4cUxeGkcC9hcnIeryurNMMcGBHp7AYlP)
- [React Information](./React.md)