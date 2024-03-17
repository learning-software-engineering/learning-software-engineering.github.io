# Getting Stylish and Responsive with Tailwind CSS

## Table of Contents

### [Introduction](#introduction)

### [Installation](#installation)

### [Usage](#usage)

### [Common Pitfalls](#commmon-pitfalls)

### [Tailwind with JavaScript Frameworks](#tailwind-with-javascript-frameworks)

### [Advantages and Limitations](#advantages-and-limitations)

### [Resources](#resources)

## Introduction

Tired of the repetitive nuances of CSS? Tailwind is a utility-first CSS framework, which allows developers to use premade styling classes without the need to write CSS classes from scratch. Tailwind provides small, single-purpose, reusable classes for spacing, lettering, and colours. These classes can then be used in HTML elements, or components from frontend libraries and frameworks.

## Installation

1. When using node, install and execute Tailwind:

```bash
npm install -D tailwindcss
npx tailwindcss init
```

2. The generated `tailwind.config.js` configuration file contains the default setup. Give Tailwind access to files by listing the template paths in the content section. For React/TypeScript web app, it can look like this:

```js
content: [
  "./pages/**/*.{ts,tsx}",
  "./components/**/*.{ts,tsx}",
  "./app/**/*.{ts,tsx}",
  "./src/**/*.{ts,tsx}",
];
```

3. Add the following to the global CSS file:

```css
@tailwind base;
@tailwind components;
@tailwind utilities;
```

Now we're set!

> **TIP:** For VSCode users, consider installing the [Tailwind CSS IntelliSense](https://marketplace.visualstudio.com/items?itemName=bradlc.vscode-tailwindcss) extension, which offers autocomplete suggestions, linting, and previews when hovering over classes. It's especially helpful for those starting out with the framework.

## Usage

### The Basics

Each Tailwind class is focused on a specific responsibility. To use a class, add it to the `class` or `className` (when using React) attribute of the element/component. For example, use the following Tailwind classes to create a div that

- occupies the full width of the screen: `w-screen`
- allows scrolling within: `overflow-scroll`
- contains a sky blue background: `bg-sky-400`
- has large text: `text-lg`

Putting it all together:

```jsx
<div className="w-screen overflow-scroll bg-sky-400 text-lg">
  {/* Some content */}
</div>
```

Start [here](https://tailwindcss.com/docs/aspect-ratio) to learn about all Tailwind classes.

When needed, add custom styles by modifying the `theme` section of `tailwind.config.js`. Here, we configure the `sm` breakpoint from 480px to 500px.

```js
module.exports = {
  theme: {
    screens: {
      //   sm: '480px',
      sm: "500px",
      md: "768px",
      lg: "976px",
      xl: "1440px",
    },
  },
};
```

To add custom styles inline, use square bracket `[]` notation. For example, if we want exactly 9px of padding, we can use:

```jsx
<div className="p-[9px]">{/* Some content */}</div>
```

Refer to [Custom Styles](https://tailwindcss.com/docs/adding-custom-styles) for more information.

### Responsive Design

Tailwind is powerful for creating a suitable experience across different devices.

#### Targeted Screen Sizes

To set a style for specific screen sizes, Tailwind offers breakpoints. These apply a style only if the screen width exceeds the breakpoint's minimum width. Breakpoints are an alternative to the traditional CSS `@media` queries.

Breakpoints:

- `sm` - 640px
- `md` - 768px
- `lg` - 1024px
- `xl` - 1280px
- `2xl` - 1536px

To denote a breakpoint, add the prefix before a class name to conditionally apply: `<breakpoint-prefix>:<class-name>`

For example, to make the height of a div 100%, on screens more than 1024 pixels wide:

```jsx
<div className="lg:h-full">{/* Some content */}</div>
```

> **NOTE:** A common mistake is to use 'sm' to target mobile devices. Mobile sizes have the smallest widths, so their styles should **not** have a breakpoint prefix.

#### Flexbox

For dynamically-sized layouts, Tailwind also provides classes for the standard [flexbox](https://tailwindcss.com/docs/flex) options, and controls for [flex-basis](https://tailwindcss.com/docs/flex-basis), on par with CSS.

### Advanced

#### Custom Plugins

Tailwind's extensibility allows you to write custom plugins to add your own utilities, components, or variants. This is particularly useful for standardizing custom designs across your projects. For example, creating a plugin for a custom button:

```jsx
// tailwind.config.js
const plugin = require("tailwindcss/plugin");

module.exports = {
  // Other configurations...
  plugins: [
    plugin(function ({ addComponents }) {
      const buttons = {
        ".btn": {
          padding: ".5rem 1rem",
          borderRadius: ".25rem",
          fontWeight: "600",
        },
        ".btn-blue": {
          backgroundColor: "#3490dc",
          color: "#fff",
          "&:hover": {
            backgroundColor: "#2779bd",
          },
        },
        // Add more button styles...
      };

      addComponents(buttons);
    }),
  ],
};
```

#### Dark Mode

Tailwind makes implementing dark mode straightforward with the dark: variant. To enable dark mode, update your tailwind.config.js:

```jsx
// tailwind.config.js
module.exports = {
  darkMode: "class", // or 'media' if you prefer to use the CSS media query
  // Other configurations...
};
```

Then, use the dark: prefix to apply styles for dark mode:

```jsx
<div class="bg-white dark:bg-gray-800">
  <!-- Content goes here -->
</div>
```

## Advantages and Limitations

### Advantages

- When using Tailwind CSS classes, developers are not restricted to a component structure and inherited styles that don't match their project. This can be problematic when using templates from component libraries such as [Bootstrap](https://getbootstrap.com). This flexibility makes Tailwind more customizable for different types of projects.
- Since each Tailwind class has atomic responsibilities, developers avoid issues where a component inherits unknown CSS styles.
- Overall, Tailwind minimizes redundant CSS code and shortens CSS files.
- Developers do not have to spend time thinking of how to apply their CSS with selectors (which can be quite tedious for larger projects).

### Limitations

- If accustomed to writing CSS, it can take some time to get used to using the equivalent Tailwind classes.
- Some projects may not need Tailwind. Using the framework requires additional overhead, which may not be worth it for small projects.
- It may take more time to complete projects, since Tailwind prioritizes styling control over pre-made components.

## Common Pitfalls

- While Tailwind encourages customization, over-relying on custom classes can lead to bloat and defeat the purpose of using a utility-first framework. Take advantage the default utility classes as much as possible before going for custom solutions.
- Don't sacrifice semantic HTML for styling convenience. Tailwind classes can and should be applied in a way that preserves the accessibility and semantics of your markup.
- To make sure your production CSS bundle is applied to the correct files, modify your content (see below) in the configuration file to ensure it contains the path(s) to all files that have any tailwind code (i.e. the use of utility classes).

```
// tailwind.config.js
module.exports = {
  content: ['./src/**/*.{js,jsx,ts,tsx,html}'],
  // Other configurations...
}
```

## Tailwind with JavaScript Frameworks

### React

Integrating Tailwind CSS with React projects streamlines the process of applying styles, allowing developers to use utility classes directly within JSX. This integration encourages a component-driven development approach, where styling can be directly tied to components for a more cohesive design and development workflow.

#### Setup (after creating your react app):

Install Tailwind CSS via npm:

```
npm install -D tailwindcss
```

Generate `tailwind.config.js`:

```
npx tailwindcss init
```

Add path to your template files in `tailwind.config.js`:

```jsx
/** @type {import('tailwindcss').Config} */
module.exports = {
  content: ["./src/**/*.{js,jsx,ts,tsx}"],
  theme: {
    extend: {},
  },
  plugins: [],
};
```

#### Using Tailwind with React

To apply Tailwind’s utility classes in a React component, use the className attribute:

```jsx
function Button() {
  return (
    <button className="bg-blue-500 hover:bg-blue-700 text-white font-bold py-2 px-4 rounded">
      Click me
    </button>
  );
}
```

This setup provides a quick, efficient method to style React applications with the flexibility of Tailwind CSS’s utility-first approach. As someone who uses React with Tailwind quite frequently, I can confidently say it has boosted my productivity by a noticeable amount.

### Vue

Tailwind CSS can seamlessly integrate with Vue.js, enhancing the styling of single-file components. The utility-first approach works well with Vue’s dynamic class bindings, allowing developers to apply conditional styles with ease.

#### Setup

Follow similar initial steps as for React to install Tailwind and generate configuration files. Ensure Tailwind processes your Vue files by correctly configuring the content option in tailwind.config.js.

#### Using Tailwind with Vue

Within Vue components, Tailwind classes are added through the class attribute, and dynamic classes can leverage Vue’s :class binding for responsive and state-driven styles:

```jsx
<template>
  <button :class="{'bg-blue-500': isActive, 'bg-red-500': !isActive}" class="text-white font-bold py-2 px-4 rounded">
    Toggle me
  </button>
</template>

<script>
export default {
  data() {
    return {
      isActive: false,
    };
  },
};
</script>
```

### Angular

#### Setup

Follow similar initial steps as for React to install Tailwind and generate configuration files. Ensure Tailwind processes your files by correctly configuring the content option in tailwind.config.js.

#### Using Tailwind with Angular

With Tailwind CSS configured, you can now begin using its utility classes within your Angular components' templates directly. For example, to style a button with Tailwind, you might write:

```jsx
<button class="bg-blue-500 hover:bg-blue-700 text-white font-bold py-2 px-4 rounded">
  Click Me
</button>
```

Angular's binding syntax works seamlessly with Tailwind, allowing you to conditionally apply styles based on component logic:

```jsx
<div [class.bg-green-500]="isActive" class="text-white p-4">
  This div changes color based on the 'isActive' property.
</div>
```

For more on Tailwind with these frameworks, on top of some topics discussed earlier in this guide, there are some links below!

## Resources

- [Learning Software Engineering: CSS](./CSS.md)
- [Official Tailwind Site](https://tailwindcss.com)
- [Extended Installation](https://tailwindcss.com/docs/installation)
- [A Friendly Video Introduction](https://www.youtube.com/watch?v=pfaSUYaSgRo)
- [Tailwind UI: A Component Library Styled with Tailwind CSS](https://tailwindui.com)
- [Defining States (Hover, Focus, and more)](https://tailwindcss.com/docs/hover-focus-and-other-states)
- [Tailwind Plugins](https://tailwindcss.com/docs/plugins)
- [Vue with Tailwind](https://www.sanity.io/guides/tailwind-css-with-vue-js)
- [Angular with Tailwind](https://nx.dev/recipes/angular/using-tailwind-css-with-angular-projects)
- [React with Tailwind](https://www.smashingmagazine.com/2020/02/tailwindcss-react-project/)
