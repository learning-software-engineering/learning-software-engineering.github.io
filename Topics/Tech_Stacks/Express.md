# Learning Express

## Table of contents
### [Introduction](#introduction)
### [Getting Started](#getting-started)
### [Core Concepts](#core-concepts)
### [Examples and Tutorials](#examples-and-tutorials)

## Introduction

Express.js is a fast, unopinionated web framework for Node.js, widely used for building web applications and RESTful APIs. Known for its simplicity and flexibility, it allows developers to create efficient server-side applications with minimal overhead. It stands out for its efficient routing system and adaptable middleware capabilities, making it a preferred choice for developers aiming to create scalable and easily manageable web applications

#### Prerequisites

Before diving into Express.js, it will be good to have a foundational understanding of certain technologies and concepts:
* Node.js: As Express.js is a framework for Node.js, it is beneficial to learn some basics of Node.js. The [Node.js Official Documentation](https://nodejs.org/en/docs/) provides a comprehensive introduction.
* JavaScript: Since Express.js is written in JavaScript, it will be good to have a solid understanding of JavaScript, especially ES6 features. [Mozilla Developer Network (MDN) JavaScript Guide](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Guide) is an place to start or refresh your JavaScript skills.
* HTTP: Familiarity with HTTP methods and status codes will be beneficial, as web development with Express.js involves handling HTTP requests and responses. The [MDN HTTP Overview](https://developer.mozilla.org/en-US/docs/Web/HTTP/Overview) offers a good explanation of HTTP concepts.

#### Official Express.js Documentation
For detailed information, best practices, and the most up-to-date guidance on using Express.js, refer to the [Official Express.js Documentation](https://expressjs.com/).

## Getting Started

#### Installation

Before installing Express.js, ensure you have Node.js installed on your system. If not, you can download and install it from [Node.js official website](https://nodejs.org/en)

Once Node.js is installed, you can install Express.js using npm. Open your command line or terminal, and run the following command:

```
npm install express --save
```

This command installs Express.js in your project directory and adds it to the list of dependencies in your package.json file.

#### Hello World Example

To demonstrate how Express.js works, let's create a simple "Hello World" application. This example will set up a basic Express.js server that responds with "Hello World" when accessed.

1. Create a Project Directory:
    First, create a new directory for your project and navigate into it:
    ```
    mkdir my-express-app
    cd my-express-app
    ```

2. Initialize Your Node.js Project:
    Initialize a new Node.js project by running:
    ```
    npm init -y
    ```
    This command creates a default package.json file in your project directory.

3. Create an Entry File:
    Create a file named index.js in your project directory. This file will serve as the entry point for your Express.js application.

4. Write the Express.js Server Code:
    Open index.js and add the following code:
    ```
    const express = require('express');
    const app = express();

    app.get('/', (req, res) => {
        res.send('Hello World');
    });

    app.listen(3000, () => {
        console.log('Express.js server running on port 3000');
    });
    ```
    This code creates an Express.js application that listens on port 3000. When you visit http://localhost:3000, it will display "Hello World".

5. Run Your Application:
    Run your application using Node.js:
    ```
    node index.js
    ```
    Visit http://localhost:3000 in your web browser, and you should see the "Hello World" message.

## Core Concepts

Below are some of the key concepts that form the foundation of Express.js.

1. Routing
    Routing refers to determining how an application responds to a client's request to a particular endpoint, which is a URI (or path) and a specific HTTP request method (GET, POST, etc.).
    * Basic Routing: Define routes using methods of the Express app object corresponding to HTTP methods. For example, `app.get()` to handle GET requests, `app.post()` for POST requests.
    * Route Parameters: Use route parameters for capturing values specified at their position in the URL.
    * Route Handlers: Provide multiple callback functions that behave like middleware to handle a request.

2. Middleware
    Middleware functions are functions that have access to the request object (`req`), the response object (`res`), and the next middleware function in the application’s request-response cycle. These functions can:
    * Execute any code
    * Make changes to the request and the response objects
    * End the request-response cycle
    * Call the next middleware in the stack

3. Request and Response Objects
    Express.js enhances the Node.js request (`req`) and response (`res`) objects with additional properties and methods, making it easier to handle HTTP requests and responses.
    * Request Object (`req`): Represents the HTTP request and has properties for the request query string, parameters, body, HTTP headers, etc.
    * Response Object (`res`): Represents the HTTP response that an Express app sends when it receives an HTTP request. It has methods for sending back responses in various formats, setting headers, etc.

## Examples and Tutorials

We'll walk through some practical examples and tutorials to demonstrate how to use key features of Express.js. These hands-on examples will help you understand how to implement different functionalities in your Express.js applications.

### Handling Forms

Express.js can easily handle form data, whether it's from a simple contact form or a complex multi-part form.

#### Basic Form Handling

In this example, we first create a basic HTML form that allows users to input a username and password. When the form is submitted, it sends a POST request to the Express.js server at the /submit-form endpoint.

On the server side, we use Express.js along with the `body-parser` middleware to handle this `POST` request. The `body-parser` middleware parses the incoming form data and makes it accessible through `req.body`. In the route handler for `/submit-form`, we extract the username and password from `req.body` and can then process this data as needed — for instance, by validating the credentials or storing them in a database.

1. HTML Form: Create a simple HTML form that posts data to your server.
```
<form action="/submit-form" method="post">
  <input type="text" name="username" placeholder="Enter Username">
  <input type="password" name="password" placeholder="Enter Password">
  <button type="submit">Submit</button>
</form>
```

2. Express.js Setup: Use the body-parser middleware to parse form data.
```
const express = require('express');
const bodyParser = require('body-parser');

const app = express();

// Middleware for parsing form data
app.use(bodyParser.urlencoded({ extended: true }));

app.post('/submit-form', (req, res) => {
  const username = req.body.username;
  const password = req.body.password;
  // Handle the form data here
  res.send(`Username: ${username}, Password: ${password}`);
});

app.listen(3000, () => console.log('Server started on port 3000'));
```

### File Uploads
Handling file uploads is another common requirement. Express.js can be integrate middleware like multer to manage file uploads effectively.

#### Basic File Upload

We start by creating an HTML form with an input field of type file. This form allows users to select a file from their device. The enctype attribute is set to `multipart/form-data`, which is necessary for uploading files via forms. When a user submits this form, it sends a `POST` request with the file data to the `/upload-file` endpoint on the server.

In the file upload setup, we use Express.js with Multer, a middleware for handling file uploads. After initializing Multer to store files in a specified directory, we create a `POST` route in Express.js to handle incoming file uploads. Multer processes the file from the form, and within the route handler, we access the file's details through `req.file`, allowing us to respond to the upload or further manipulate the file as needed.

1. HTML Form for File Upload:
```
<form action="/upload-file" method="post" enctype="multipart/form-data">
  <input type="file" name="myFile">
  <button type="submit">Upload</button>
</form>
```

2. Express.js and Multer Setup:
```
const express = require('express');
const multer = require('multer');
const upload = multer({ dest: 'uploads/' });

const app = express();

app.post('/upload-file', upload.single('myFile'), (req, res) => {
  const file = req.file;
  // Handle the uploaded file here
  res.send(`File uploaded: ${file.originalname}`);
});

app.listen(3000, () => console.log('Server started on port 3000'));
```
