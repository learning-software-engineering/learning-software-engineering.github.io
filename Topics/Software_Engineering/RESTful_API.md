# RESTful API Standard

## Table of Contents:
#### [Introduction](#introduction)
#### [What is REST?](#what-is-rest)
#### [Principles of REST](#principles-of-rest)
#### [Resource](#resource)
#### [HTTP Methods](#http-methods)
#### [Status Codes](#status-codes)

## Introduction
<a id='introduction'></a>
This document provides guidelines and examples for the web APIs that adhere to the Representational State Transfer (REST) architectural style.

## What is REST?
<a id='what-is-rest'></a>
**Representational State Transfer (REST)** is a set of guidelines for designing software systems for the Internet. It’s like a blueprint for building the World Wide Web. It lays out rules to ensure that different parts of the web (like websites or apps) can talk to each other efficiently and securely.

## Principles of REST
<a id='principles-of-rest'></a>
- **Uniform Interface**:
  - The method of communication between the client and the server should be uniform.
  - Resource representation should follow specific guidelines like certain naming conventions or data formats.
  - Clients should be able to navigate the whole site when they have access to the initial URI
- **Client-Server**:
  - The client and the server should act independently. They interact with each other only through requests and responses.
  - Client and server should be implemented so that they do not need prior information to communicate with each other.
    - This way, the code of each side can be modified without affecting each other.
- **Stateless**:
  - Each request from a client to a server must contain all the information needed to understand and process the request.
  - The server does not store anything about requests made by the client, it treats all requests as new.
  - If the client app needs to be stateful, each request must contain all information necessary, like authentication details.
- **Cacheable**:
  - Responses from the server can be cached by the client to improve performance.
  - Response needs to explicitly label itself as cacheable or non-cacheable
- **Layered System**:
  - Allow architecture to be composed of hierarchical layers
  - Each component cannot see beyond the immediate layer that they are interacting with.
  - an example: *MVC pattern*
- **Code on Demand**:
  - (Optional)
  - Allow returning executable code to the client
  - Reduce the number of features needed to be pre-implemented

## Resource
<a id='resource'></a>
- Any information can be considered a resource.
- REST uses resource identifiers to identify each resource involved in the interactions
- Resource representations shall be self-descriptive
  - Media Types have no relation to the resource methods GET/PUT/POST/DELETE/

## HTTP Methods
<a id='http-methods'></a>
- **GET**: Retrieves resources.
- **POST**: Sends data to the server to create a new resource.
- **PUT**: Updates a resource.
- **DELETE**: Deletes a resource.

## Status Codes
<a id='status-codes'></a>
- **200 OK**: The request was successful.
- **201 Created**: The request was successful and a resource was created as a result.
- **400 Bad Request**: The request could not be understood or was missing the required parameters.
- **404 Not Found**: The requested resource could not be found.
- **500 Internal Server Error**: An error occurred on the server.

## Example
API Endpoint: "/books" <br><br>
&nbsp; Method: **GET**
    - This method retrieves all books. <br>
  - Response
    - 200 OK on success, together with a JSON message that lists all books.
    - 404 Not Found if no books are found<br><br>
  
&nbsp; Method: **POST**
    - This method creates a new book. <br>
  -  Request
    -  JSON object with title and author
  - Response
    - 201 Created on success
    - 400 Bad Request if the request is not valid <br><br>

API Endpoint: "/books/{id}" <br><br>
&nbsp; Method: **GET**
    - This method retrieves the book with {id}. <br>
  - Response
    - 200 OK on success, together with a JSON message that includes a book with {id}.
    - 404 Not Found if the book is not found<br><br>
  
&nbsp; Method: **PUT**
    - This method updates the existing book with {id}. <br>
  -  Request
    -  JSON object with title and author
  - Response
    - 200 OK on success
    - 400 Bad Request if the request is not valid
    - 404 Not Found if the book is not found<br><br>
    
&nbsp; Method: **DELETE**
    - This method deletes the existing book with {id}. <br>
  -  Request
    -  JSON object with title and author
  - Response
    - 200 OK on success
    - 404 Not Found if the book is not found
