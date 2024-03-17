# An introduction to Chakra UI

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
