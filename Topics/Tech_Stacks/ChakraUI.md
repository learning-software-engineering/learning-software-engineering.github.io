# An introduction to Chakra UI

## Introduction

Chakra UI is a UI component library specifically designed for React. It provides a comprehensive set of pre-styled components ranging from basic layout components to advanced form inputs, modals, loading bars, and many more. Chakra UI has a powerful and React-forward prop-based styling system that easily allows for responsive design as well as a high degree of customizability.

Chakra UI also has a strong focus on theming and customizability, allowing for a high degree of control and consistency over an application's look and feel. It also provides many quality of life utilities that make frontend development faster and more efficient, such as a built-in dark mode, and a comprehensive set of responsive design tools.

This guide will cover the basics of Chakra UI, including installation, setup, usage, the benefits and drawbacks of using Chakra UI, and further reading.

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
import * as React from "react";

// 1. import `ChakraProvider` component
import { ChakraProvider } from "@chakra-ui/react";

function App() {
  // 2. Wrap ChakraProvider at the root of your app
  return (
    <ChakraProvider>
      <TheRestOfYourApplication />
    </ChakraProvider>
  );
}
```

A list of components and their custom props can be found [here](https://chakra-ui.com/docs/components).

## Usage

### Design principles

Chakra UI employs several key design principles:

- **Prop-based styling**: a component's style can be customized by passing in a prop corresponding to a CSS property.
- **Responsive-forward design**: responsive design is both easy to implement and highly customizable as a result of Chakra UI's seamless integration of media queries and breakpoints to custom styling
- **Dark mode**: custom styling for both light and dark modes is closely integrated into Chakra UI's styling system
- **Simple and intuitive API**: Chakra UI's API is designed to be simple and intuitive, making it easy to use and understand. Moreover, it is designed to reduce clutter and make development faster, while maintaining well-structured and readable code.

### Using UI components

Chakra UI provides a plethora of pre-styled components that cover a wide range of UI needs. These components are highly customizable and can be easily integrated into your React application.

**Basic Usage**:
To use a Chakra UI component, simply import it from `@chakra-ui/react` and use it as you would any other React component. For example, to use a `Button` component:

```js
import { Button } from "@chakra-ui/react";

function MyComponent() {
  return <Button colorScheme="blue">Click me</Button>;
}
```

### Styling components

A component's style can be customized by passing certain props to it. The props that are accepted rougly correspond to CSS properties, and accept any value that CSS accepts.

For example, the following creates a button with styling that corresponds to the CSS property `margin-left: 10px;`

```jsx
<Button marginLeft={"30px"}>hello</Button>
```

To make development faster and reduce code clutter, many commonly used props also have abbreviated aliases that are shorter and more legible. For example, in the above example, `ml` is the abbreviated alias of `marginLeft`, so it would be equivalent to:

```jsx
<Button ml={"30px"}>hello</Button>
```

<img src="https://github.com/learning-software-engineering/learning-software-engineering.github.io/assets/40612523/58ea0265-e23f-4db7-a831-6417b2530b71">

A list of props, their aliases, as well as their corresponding CSS class can be found [here](https://chakra-ui.com/docs/styled-system/style-props).

Pseudo classes also exist in this styled prop system. Pseudo classes are differentiated with an underscore at the beginning of the prop and they accept an object of prop name and value key-value pairs. For example, the following creates a button which changes the background to red when hovered over:

```jsx
<Button _hover={{ bg: "red" }}>hello</Button>
```

<img src="https://github.com/learning-software-engineering/learning-software-engineering.github.io/assets/40612523/d0b865df-d256-4404-8e47-c9df86f83503">

Other common pseudo classes would include `_active`, `_focus`, `_before`, etc. A full list of pseudo classes can be found [here](https://chakra-ui.com/docs/styled-system/style-props#pseudo)

### Responsiveness

Chakra UI's responsive design is highly customizable and easy to implement. The `width` style prop, for example, can accept an object of prop name and value key-value pairs, where the key is a breakpoint and the value is the prop value. By default, the breakpoints correspond to pre-defined sizes corresponding to the min-width of the screen (e.g. `base: "0em"`, `sm: "30em"`, `md: "48em"`, etc.). For example, the following creates a box with a width of 100% on screens smaller than 30em (mobile) and 50% on screens larger than 30em (desktop):

```jsx
<Box width={{ base: "100%", sm: "50%" }}>hello</Box>
```

Chakra UI also has a shorthand for responsive design, where the prop value is an array of values, where the first value corresponds to the base value and the second value corresponds to the value at the first breakpoint. For example, the following creates a box with a width of 100% on screens smaller than 30em (mobile) and 50% on screens larger than 30em (desktop):

```jsx
<Box width={["100%", "50%"]}>hello</Box>
```

Breakpoints can also be customized using the `theme` object, allowing for a higher degree of control over responsive design. A full list of breakpoints and their default values can be found [here](https://chakra-ui.com/docs/styled-system/responsive-styles#customizing-breakpoints).

### Theming

Chakra UI's theming system is highly customizable and allows for a high degree of control over the look and feel of your application. The `ChakraProvider` component accepts a `theme` prop, which is an object that contains the theme configuration. The theme object can be customized to include custom colors, fonts, breakpoints, and more. For example, the following creates a custom theme with custom colors:

```jsx
// 1. Import `extendTheme`
import { extendTheme } from "@chakra-ui/react"

// 2. Call `extendTheme` and pass your custom values
const theme = extendTheme({
  colors: {
    brand: {
      100: "#f7fafc",
      // ...
      900: "#1a202c",
    },
  },
})

// 3. Pass the new theme to `ChakraProvider`
<ChakraProvider theme={theme}>
  <App />
</ChakraProvider>

// 4. Now you can use these colors in your components
function Usage() {
  return <Box bg="brand.100">Welcome</Box>
}
```

This example was taken from the [documentation on custom theming](https://chakra-ui.com/docs/styled-system/customize-theme). This page contains more information on customizing themes and providesa comprehensive list of the theme configuration options.

## Benefits and Drawbacks

### Benefits

- **Accessibility**: Chakra UI prioritizes accessibility, ensuring that components are usable by everyone, including those with disabilities.
- **Easy to Build Complex Interfaces**: Chakra UI's component-based architecture follows a modular approach, meaning complex interfaces can be easily created through composing smaller, reusable components.
- **Intuitive Documentation\***: The developer experience of Chakra UI is strong through Chakra UI's intuitive and clear [documentation](https://chakra-ui.com/docs/styled-system/style-props). This means, important explanations, for concepts such as responsive design and styling, can always be easily understood and found.
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
