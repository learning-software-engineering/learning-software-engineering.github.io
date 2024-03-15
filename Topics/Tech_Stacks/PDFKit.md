# Introduction to PDFKit


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
// Add a link
doc.link(100, 100, 200, 20, 'http://example.com'); // Position (x: 100, y: 100), Size (width: 200, height: 20), URL

// Add a highlight annotation
doc.highlight(100, 150, 200, 25, { annotationFlags: 'NoView' }); // Position (x: 100, y: 150), Size (width: 200, height: 25)

// Adding text note annotation
doc.text('Note: ', 100, 200)
   .annotate(100, 200, 100, 15, {
     type: 'Text',
     title: 'Reminder',
     contents: 'Remember to check this part of the document.',
     open: true
   });
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
