# API Documentation with SwaggerHub

## Table of Contents
- [Brief Outline of APIs ](#brief-outline-of-apis)
- [Purpose of API Documentation](#purpose-of-api-documentation)
- [Keys to Good API Documentation](#keys-to-good-api-documentation)
- [Introduction of SwaggerHub](#introduction-of-swaggerhub)
  - [Features](#features)
- [Other Free Tool](#other-free-tool)

## Brief Outline of APIs
API stands for application programming interface and from "is a set of defined rules that enable different applications to communicate with each other" ([IBM](https://www.ibm.com/topics/api)).

Two main aspects of APIs:
- endpoint: the location where a subset of the API's functions can be accessed 
  - ex. a URL
- method: clarifies what type of API function is desired
  - ex. a POST method implies the user wants to create or add something

For more information, click [here](https://www.postman.com/what-is-an-api/).

## Purpose of API Documentation
As the name suggests, API documentation describes a handbook of instructions and expectations around working with the project's APIs. 
This allows the user to easily and accurately interact with the API.
This is super important for projects with different people who are creating and using the API, including a front-end and backend team, your group and your partner, or even you and future you!

## Key to Good API Documentation
- proofread for correct spelling and grammar 
- ensure the technical background needed to understand is reasonable
- cover all the basics of each endpoint:
  - what methods each endpoint supports
  - what is accepted and/or what is returned from each endpoint
    - including sample responses and errors
- update the documentation when changes are made to the code
- consistent format to allow easy access to relevant information

## Introduction of SwaggerHub
[SwaggerHub](https://swagger.io/tools/swaggerhub/) is one tool created to make API documentation easy to edit and read. 

### Features
- easy to edit: can use code or visual editor on their website and undo changes to previous revisions
- easy to learn: there are many resources, [example](https://support.smartbear.com/swaggerhub/docs/en/get-started/basics-of-swaggerhub.html)
- easy to share: by default, the API documentation is accessible by a public link, or the contents can be exported to a html file, json, etc.
- easy to organize: can group endpoints and methods by tags
- easy to standardize: specifications for each endpoint will follow a specific order and schemas can be created for outputs or inputs of the same format
  - a schema on SwaggerHub is like an object in Python andd has attributes and types
- easy to iterate: can create multiple versions, fork, and even merge API documents
- interactive: can generate sample requests and outputs from the link to the API
- free: the above features can all be accessed for free, however adding a collaborator requires the enteprise plan

## Other Free Tools
While SwaggerHub is a great resource, there are also other options that create great API documents.
- Autogenerate API documentation: [Postman](https://learning.postman.com/docs/publishing-your-api/api-documentation-overview/)
- Keep software documentation and API documentation together [document360](https://document360.com/pricing/#)
- Deploying API on a specific website: [redoc](https://redocly.com/redoc/)