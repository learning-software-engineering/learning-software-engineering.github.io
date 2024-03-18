# Embedded JavaScript (EJS): Simplifying Web Development with Dynamic Content

Embedded JavaScript (EJS) is a powerful templating language that simplifies the process of dynamically generating HTML content. In this tutorial, we'll explore the basics of EJS and delve into some of the more advanced functionality that will enable you to create dynamic and interactive web pages.

## Requirements

EJS works seamlessly across various platforms, including Windows, Mac, and Linux, and is compatible with both Python 2 and 3. Ensure you have Python installed before proceeding. You can refer to the official Python website for installation instructions. This tutorial demonstrates examples using Python 3.

## Introduction to Embedded JavaScript

Embedded JavaScript (EJS) allows developers to embed JavaScript code directly within their HTML markup. Unlike other traditional templating languages, EJS leverages JavaScript's expressive syntax which allows for a seamless integration of the server-side logic with the client-side views.

## What Can You Achieve with EJS?

EJS empowers developers to accomplish a wide array of tasks, including:

- **Dynamic Content Generation**: Effortlessly generate dynamic content by embedding JavaScript expressions within HTML templates.
  
- **Conditional Rendering**: Implement conditional logic to selectively render content based on specified criteria

- **Data Binding**: Bind server-side data to client-side views, facilitating the presentation of dynamic information to users.

- **Iterative Rendering**: Iterate over data collections to dynamically generate HTML elements, enabling the creation of dynamic lists, tables, and more.

## Installation

Before using EJS, you need to install it. You can install EJS via npm, the Node.js package manager, using the following command:

```bash
npm install ejs
```

## Getting Started

To begin using EJS, create a new HTML file and import the EJS library:
```html
<script src="ejs.min.js"></script>
```

## Basic Syntax and Usage
EJS employs a very simple but powerful syntax to embed JavaScript code within HTML markup. Below are some of the fundamental concepts:

- **Interpolation: Use <%= %> tags to insert the result of a JavaScript expression into the HTML document.

- **Conditional Statements: Use <% if (condition) { %> ... <% } %> blocks to implement conditional rendering based on specific conditions.

- **Iterative Rendering: Use <% for (let item of items) { %> ... <% } %> constructs to iterate over data collections and generate dynamic content.

## Advanced Features
Beyond the basics, EJS offers advanced features to further enhance your web development workflow:

- **Partials: Convert your templates into modules by creating reusable partials which enables you to reuse your code and make it look more presentable, similar to React components

- **Layouts: Define master layouts to encapsulate common page structures and streamline the creation of consistent user interfaces.

- **Custom Functions: Extend EJS functionality by defining custom JavaScript functions and incorporating them into your templates.

## Example Usage
In this section we see how some of these functionalities are used

This is an example of a partial:
```html
</div>
<div class="footer-padding"></div>
  <div class="footer">
    <p>Copyright</p>
  </div>
</div>
</body>
</html>
```

This footer can be reused in any other pages by including this line whereever the footer is needed. 

```html
<%- include("partials/header") %>

<h1><%= postHeader %></h1>
<p> <%= postContent %> </p>

<%- include("partials/footer") %>
```

In this example, we include the header, have some custom content, and then have the footer. This also shows how interpolation is used to display the variables postHeader and postContent which are passed in as JSON objects by the server. 

Below we see an example of iterative rendering:
```html
<% posts.forEach(function(post) { %>
  <h1> <%= post.title %></h1>
  <p>
    <%= post.content.substring(0, 100) + " ..."%>
    <a href="/posts/ <%=post.title %>">Read More</a>
  </p>
<% }) %>
```

It may also be a useful addition to see how the server is interacting with these pages, so some code examples are given below, note how the variables are passed in and used.

```html
app.get("/", function (req, res) {
  res.render("home", {homeStartingContent: homeStartingContent, posts: posts})
})
```

One of the key advantages of EJS can also be seen through the following code sample:
```html
app.get("/posts/:postName", function (req, res) {

  posts.forEach(function(post) {
    if (_.lowerCase(post.title) === _.lowerCase(req.params.postName)) {
      res.render("post", {postHeader: post.title, postContent: post.content})
    }
  })

})
```

In this example we can see that for each post in the database, we dynamically create a new page posts/postName, wherein each page has the same exact format, just the content is differed depending on the post itself. 


## Learn More

- **https://ejs.co/#install
- **https://www.digitalocean.com/community/tutorials/how-to-use-ejs-to-template-your-node-application
