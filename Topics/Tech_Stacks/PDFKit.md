# Introduction to PDFKit
## Table of Contents
- [Introduction](#introduction)
- [Getting Started](#getting-started)
  - [Installation](#installation)
  - [Basic Usage](#basic-usage)
- [Features](#features)
  - [Text](#text)
  - [Images](#images)
  - [Vector Graphics](#vector-graphics)
  - [Annotations](#annotations)
- [Advanced Usage](#advanced-usage)
  - [Custom Fonts](#custom-fonts)
  - [Multipage Support](#multipage-support)
  - [Performance](#performance)
- [Conclusion](#conclusion)
- [References](#references)

## Introduction

PDFKit is a powerful PDF document generation library for Node.js and the browser. It enables developers to create complex PDFs from scratch or manipulate existing PDF documents. PDFKit provides an extensive set of features, including text, images, vector graphics, and more, making it suitable for a wide range of applications, from dynamic invoice generation to creating ebooks and reports.


## Getting Started

### Installation

To use PDFKit in your project, you first need to install it through npm, Node.js's package manager. Open your terminal and run:

```bash
npm install pdfkit
```

### Basic Usage

Here's a simple example of generating a PDF document with PDFKit:

```javascript
// Import PDFKit
const PDFDocument = require('pdfkit');
const fs = require('fs');

// Create a document
const doc = new PDFDocument();

// Pipe the document to a blob
doc.pipe(fs.createWriteStream('output.pdf'));

// Add some content
doc.fontSize(25).text('Hello, World!', 100, 100);

// Finalize the document and end the stream
doc.end();
```

This code creates a PDF file named `output.pdf` with the text "Hello, World!".

## Features

### Text

PDFKit allows you to add text with various styles and alignments. You can customize the font size, color, and type.
```javascript
// Add custom styled text
doc.fontSize(18) // Set font size
   .font('Times-Roman') // Set font type
   .fillColor('blue') // Set text color
   .text('Hello, World!', 100, 100); // Add text at position (x: 100, y: 100)
```
![Output of code snippet](./PDFKit_Graphics/image1.png)


### Images

Adding images to your PDF is straightforward. PDFKit supports JPEG and PNG formats. You can control the positioning and scaling of images.
```javascript
// Add an image
const imagePath = 'path/to/image.png'; // Path to your image
doc.image(imagePath, 50, 150, { width: 300, height: 150 }); // Position (x: 50, y: 150) and scale to width 300, height 150
```
### Vector Graphics

PDFKit excels at drawing shapes and paths, enabling you to add lines, circles, and arbitrary paths to your documents.
```javascript
// Draw a line
doc.moveTo(100, 200) // Start point
   .lineTo(300, 200) // End point
   .stroke();

// Draw a circle
doc.circle(100, 300, 50) // Center (x: 100, y: 300), Radius: 50
   .fill('red'); // Fill color

// Arbitrary path (drawing a triangle here)
doc.moveTo(100, 350) // Start at this point
   .lineTo(150, 400) // Line to this point
   .lineTo(50, 400) // Line to this point
   .closePath() // Connect end to start
   .stroke(); // Stroke the path
```
### Annotations

You can include links, notes, and highlights in your PDF files, making it perfect for interactive documents.
```javascript
// Set the font size and fill color, then add text at position (x: 20, y: 20)
doc.fontSize(25)
   .fillColor('blue')
   .text('This is a link!', 20, 20);

// Measure the width and height of the string 'This is a link!' to use in annotations
const width = doc.widthOfString('This is a link!');
const height = doc.currentLineHeight();

// Add an underline beneath the text and a hyperlink annotation that links to 'http://google.com/'
// The underline and link cover the area defined by the text's width and height
doc.underline(20, 20, width, height, {color: 'blue'})
   .link(20, 20, width, height, 'http://google.com/');

// Set the fill color to red, then add a highlight annotation behind the text 'Hello World!'
// Following this, the text 'Hello World!' is added.
// The highlight covers the width of 'Hello World!' text and a fixed height of 25 units starting from the current document position (doc.y)
doc.fillColor('red').highlight(20, doc.y, doc.widthOfString('Hello World!'), 25).text("Hello World!");

```

## Advanced Usage

### Custom Fonts

PDFKit supports custom fonts in TrueType (.ttf), OpenType (.otf), WOFF, and SVG formats. This feature allows for a wide range of typographic options.

### Multipage Support

PDFKit automatically handles page creation and management, allowing for dynamic document generation that spans multiple pages.

### Performance

For large or complex documents, PDFKit offers performance optimizations, such as streamlining vector graphics and efficiently managing memory usage.



## Conclusion

PDFKit is a versatile tool for PDF generation, offering a broad set of features for creating complex documents. Its ability to work both in Node.js environments and the browser makes it an excellent choice for a variety of applications. Whether you're generating reports, invoices, or custom documents, PDFKit provides the flexibility and power needed to create high-quality PDFs.

## References

- PDFKit Official Website: [http://pdfkit.org/](http://pdfkit.org/)
- GitHub Repository: [https://github.com/foliojs/pdfkit](https://github.com/foliojs/pdfkit)
