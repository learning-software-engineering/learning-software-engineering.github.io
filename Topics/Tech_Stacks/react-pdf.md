# Using react-pdf library

### Introduction

react-pdf is a npm package that allows you to display a customized pdf on your react website. This page will give you an introduction to install and display a simple pdf and also give you an idea of what you can expect from using this package.

offical document: https://react-pdf.org/

### Install

You can only use this library in a react project, so you need to install node, npm, and react first, you can read more in here: https://learning-software-engineering.github.io/Topics/Tech_Stacks/React.html

To install this package, do `npm install @react-pdf/renderer --save`

### component structure

after installing, you can import the provided components

```
import React from 'react';
import { Page, Text, View, Document, StyleSheet } from '@react-pdf/renderer';
```

a pdf component looks like this

```
const styles = StyleSheet.create({
  page: {
    flexDirection: 'row',
    backgroundColor: '#E4E4E4'
  },
  section: {
    margin: 10,
    padding: 10,
    flexGrow: 1
  }
});

const MyDocument = () => (
  <Document>
    <Page size="A4" style={styles.page}>
      <View style={styles.section}>
        <Text>Section #1</Text>
      </View>
      <View style={styles.section}>
        <Text>Section #2</Text>
      </View>
    </Page>
  </Document>
);
```

we can display this document in a pdf viewer

```
import React from 'react';
import ReactDOM from 'react-dom';
import { PDFViewer } from '@react-pdf/renderer';

const App = () => (
  <PDFViewer>
    <MyDocument />
  </PDFViewer>
);
```

Note that this library has it's own style API, traditional CSS does not work inside the `MyDocument` component, you need to use the `StyleSheet` component provided by the library, which is very similar to the original CSS.

### Tags

`<Document>` is the most outer tag, it is the wrapper tag for a pdf document.

`<Page>` tag is the wrapper for one page in the pdf.

`<View>` tag is a division inside a page and can be viewed as the `<div>` equivalent in html.

`<Text` is the most specific component inside the document.

### Styles

As in the example component, we used a `StyleSheet` object to wrap the styles for different tags, we can get around this by using in-line style like `<Text style={{ marginLeft: 3, marginRight: 3 }}>`

This package provides a lot of customizations:

- background color: `<Page size="A4" style={{ backgroundColor: "FFFFFF"}}`
- font size: `<Page size="A4" style={{fontSize: 10}}`
- font family `<Page size="A4" style={{fontFamily: "Roboto"}}`

and many more you can find on the official website: https://react-pdf.org/styling

### Limitations

- we cannot easily bold a part of text, it requires intalling a bold font library.
- default font families are limited, and additional font families requires downloading them or obtain a font library url

### Example project

you can also check an example website I wrote using this library, this website uses react-pdf to power a resume generator

- github repo: https://github.com/Ratbuyer/resume-builder
- deployed url: https://resumedev.site/
