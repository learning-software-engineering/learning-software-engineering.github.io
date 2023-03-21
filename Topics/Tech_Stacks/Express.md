# Setting up a Basic RESTful Server with Node.js and Express

## Table of contents

### [Introduction](#introduction-1)

### [Prerequisites](#prerequisites-1)

### [Setting up the project](#setting-up-the-project-1)

### [Installing Express](#installing-express-1)

### [Creating a basic server](#creating-a-basic-server-1)

### [Defining RESTful routes](#defining-restful-routes-1)

## Introduction

This guide will help you set up a simple RESTful server using Express, a popular web framework for Node.js. We will create a basic server that listens for HTTP requests and sends responses.

## Prerequisites

[Node.js](https://nodejs.org/en/download)
[npm](https://www.npmjs.com/package/npm)

## Setting up the project

First, let's create a new directory for our project and navigate to it using the terminal.

```bash
mkdir express-server
cd express-server
```

Now, initialize the project with the `npm init` command. Follow the prompts or use `npm init -y` to accept the defaults.

```bash
npm init -y
```

## Installing Express

To install Express, run the following command:

```bach
npm install express
```

## Creating a basic server

Create a new file named `app.js` in the project directory and add the following code:

```javascript
const express = require("express");
const app = express();
const PORT = process.env.PORT || 3000;

app.get("/", (req, res) => {
  res.send("Hello, World!");
});

app.listen(PORT, () => {
  console.log(`Server is running on port ${PORT}`);
});
```

This code imports the Express library, creates an instance of it, and sets up a basic server that listens on port 3000.

## Defining RESTful routes

Next, we'll define some RESTful routes for a simple resource. For this example, we'll use an in-memory array to represent a list of items.

Add the following code to `app.js`:

```javascript
const items = [];

app.use(express.json());

app.get("/items", (req, res) => {
  res.json(items);
});

app.post("/items", (req, res) => {
  const newItem = req.body;
  items.push(newItem);
  res.status(201).json(newItem);
});

app.get("/items/:id", (req, res) => {
  const id = parseInt(req.params.id);
  const item = items.find((i) => i.id === id);

  if (!item) {
    return res.status(404).json({ error: "Item not found" });
  }

  res.json(item);
});

app.put("/items/:id", (req, res) => {
  const id = parseInt(req.params.id);
  const index = items.findIndex((i) => i.id === id);

  if (index === -1) {
    return res.status(404).json({ error: "Item not found" });
  }

  items[index] = req.body;
  res.json(items[index]);
});

app.delete("/items/:id", (req, res) => {
  const id = parseInt(req.params.id);
  const index = items.findIndex((i) => i.id === id);

  if (index === -1) {
    return res.status(404).json({ error: "Item not found" });
  }

  const deletedItem = items.splice(index, 1)[0];
  res.json(deletedItem);
});
```

We have defined the following routes for our items resource:

`GET /items`: Retrieve all items \
`POST /items`: Create a new item \
`GET /items/`:id: Retrieve a specific item by ID \
`PUT /items/`:id: Update an existing item by ID \
`DELETE /items/`:id: Delete an item by ID \
The `app.use(express.json());` line tells Express to parse incoming JSON payloads, allowing us to access the request body data.
