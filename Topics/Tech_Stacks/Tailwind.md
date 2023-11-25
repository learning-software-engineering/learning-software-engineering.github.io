# Getting Stylish and Responsive with Tailwind CSS

## Table of Contents
### [Introduction](#introduction)
### [Installation](#installation)
### [Usage](#usage)
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
   './pages/**/*.{ts,tsx}',
   './components/**/*.{ts,tsx}',
   './app/**/*.{ts,tsx}',
   './src/**/*.{ts,tsx}',
 ]
```

3. Add the following to the global CSS file:
```css
@tailwind base;
@tailwind components;
@tailwind utilities;
```

Now we're set!

> **TIP:**  For VSCode users, consider installing the [Tailwind CSS IntelliSense](https://marketplace.visualstudio.com/items?itemName=bradlc.vscode-tailwindcss) extension, which offers autocomplete suggestions, linting, and previews when hovering over classes. It's especially helpful for those starting out with the framework.


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
      sm: '500px',
      md: '768px',
      lg: '976px',
      xl: '1440px',
    }
  }
}
```

To add custom styles inline, use square bracket `[]` notation. For example, if we want exactly 9px of padding, we can use:
```jsx
<div className="p-[9px]">
   {/* Some content */}
</div>
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
<div className="lg:h-full">
    {/* Some content */} 
</div>
```

> **NOTE:** A common mistake is to use 'sm' to target mobile devices. Mobile sizes have the smallest widths, so their styles should **not** have a breakpoint prefix. 

#### Flexbox
For dynamically-sized layouts, Tailwind also provides classes for the standard [flexbox](https://tailwindcss.com/docs/flex) options,  and controls for [flex-basis](https://tailwindcss.com/docs/flex-basis), on par with CSS.

## Advantages and Limitations
### Advantages
- When using Tailwind CSS classes, developers are not restricted to a component structure and inherited styles that don't match their project. This can be problematic when using templates from component libraries such as [Bootstrap](https://getbootstrap.com). This flexibility makes Tailwind more customizable for different types of projects.
- Since each Tailwind class has atomic reponsibilities, developers avoid issues where a component inherits unknown CSS styles.
- Overall, Tailwind minimizes redundant CSS code and shortens CSS files.

### Limitations
- If accustomed to writing CSS, it can take some time to get used to using the equivalent Tailwind classes. 
- Some projects may not need Tailwind. Using the framework requires additional overhead, which may not be worth it for small projects.
- It may take more time to complete projects, since Tailwind prioritizes styling control over pre-made components.


## Resources
- [Learning Software Engineering: CSS](./CSS.md)
- [Official Tailwind Site](https://tailwindcss.com)
- [Extended Installation](https://tailwindcss.com/docs/installation)
- [A Friendly Video Introduction](https://www.youtube.com/watch?v=pfaSUYaSgRo)
- [Tailwind UI: A Component Library Styled with Tailwind CSS](https://tailwindui.com)
- [Defining States (Hover, Focus, and more)](https://tailwindcss.com/docs/hover-focus-and-other-states)
