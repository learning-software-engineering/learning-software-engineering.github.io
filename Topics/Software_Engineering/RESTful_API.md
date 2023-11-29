# RESTful API Standard

## Introduction

This document provides guidelines and examples for the web APIs that adhere to the Representational State Transfer (REST) architectural style.

## What is REST?

**Representational State Transfer (REST)** is a set of guidelines for designing software systems for the internet. It’s like a blueprint for building a city, but for the World Wide Web. It lays out rules to ensure that different parts of the web (like websites or apps) can talk to each other efficiently and securely.

## Principles of REST

- **Client-Server**: This principle establishes that the client and the server should act independently. They interact with each other only through requests and responses.
- **Stateless**: Each request from a client to a server must contain all the information needed to understand and process the request.
- **Cacheable**: Responses from the server can be cached by the client to improve performance.
- **Uniform Interface**: The method of communication between the client and the server should be uniform.

## HTTP Methods

- **GET**: Retrieves resources.
- **POST**: Sends data to the server to create a new resource.
- **PUT**: Updates a resource.
- **DELETE**: Deletes a resource.

## Status Codes

- **200 OK**: The request was successful.
- **201 Created**: The request was successful and a resource was created as a result.
- **400 Bad Request**: The request could not be understood or was missing required parameters.
- **404 Not Found**: The requested resource could not be found.
- **500 Internal Server Error**: An error occurred on the server.