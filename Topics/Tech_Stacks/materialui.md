# Material UI Guide

## Introduction

Material UI (MUI) is the most popular UI framework for React.

It is an open-source library containing a large amount of components that can be seamlessly integrated into React applications to create a customizable user experience. MUI components are responsive, allowing for consistency across different screen sizes and platforms.

## Installation

Since MUI is a framework for React, ensure that dependencies `react` and `react-dom` are installed. They can be installed with `npm install react` and `npm install react-dom` respectively.

To install MUI using npm, run the console command `npm install @mui/material @emotion/react @emotion/styled`

To install with yarn, run `yarn add @mui/material @emotion/react @emotion/styled`

## Importing Components

Material UI components can be imported individually. For example, a `Button` component can be added to a .jsx file with the following:

```js
import Button from '@mui/material/Button';
```

Multiple components can be imported like this:

```js
import {
    Box,
    Button,
    Grid,
} from '@mui/material';
```

## Adding Components

MUI components are utilized in a similar way to HTML in React JSX, with its own unique tags. MUI components are diffentiated from HTML with their capitalized tag names. Some components have variants that affect their styling.

```js
export default function ButtonUsage() {
  return <Button variant="contained">Hello world</Button>;
}
```

## Styling Components

The styling of a component can be changed in serveral ways:

### One-off customization

To style one instance of a component, you can use the sx prop:

```js
<Button variant="contained" sx={{ color: '#76ABAE'}}>Hello world</Button>
```

### Reusable component

Using the `styled()` utility, you can create a reusable component which appears consistently across the application:

```js
import * as React from 'react';
import Slider from '@mui/material/Slider';
import { styled } from '@mui/material/styles';

const HelloWorldButton = styled(Button)({
  color: '#76ABAE'
});

export default function StyledCustomization() {
  return <HelloWorldButton>Hello world</HelloWorldButton>;
}
```

## Mobile Rendering

Material UI components are primarily developed for mobile devices, which are then scaled up for larger viewports. It is highly recommended to add the viewport meta tag, which ensures proper rendering and touch zooming for all devices.

`<meta name="viewport" content="initial-scale=1, width=device-width" />`

## References

For a detailed introductory guide to Material UI with usage examples, visit https://mui.com/material-ui/getting-started/