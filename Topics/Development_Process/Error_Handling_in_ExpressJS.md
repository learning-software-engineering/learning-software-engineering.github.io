# Graceful Error Handling in Express
## Table of Contents
1. [Introduction](#introduction)
2. [Goals of Error Handling for RESTful APIs](#goals-of-error-handling-for-restful-apis)
3. [Error Handling Middleware](#error-handling-middleware)
4. [Custom Error Objects](#custom-error-objects)
    - [Status Codes](#status-codes)
    - [Implementing a Custom Error class](#implementing-a-custom-error-class)
    - [Example Usage](#example-usage)
5. [Conclusion](#conclusion)

## Introduction
[Express.JS](../Tech_Stacks/Express.md) (aka Express) is a scalable backend web framework for building [RESTful APIs](https://aws.amazon.com/what-is/restful-api/#:~:text=RESTful%20API%20is%20an%20interface,applications%20to%20perform%20various%20tasks.) with [Node.JS](../Tech_Stacks/NodeJS_Intro.md). It provides a variety of interelated features for server-side API development, including support for routing, middleware, templating (e.g. with EJS and Handlebars), static file serving and utilities for managing HTTP request-response flows. Error handling is an important aspect of any sofware project as it is critical for development, maintainability and functionality. It is especially important when building RESTful APIs where there exists specific expectations of how erroneous scenarios should be handled, such as setting appropriate status codes in response objects, returning error information in a consistent format etc.

This guide aims to highlight the mechanisms in Express that afford graceful error handling and how they can be utilised with good practices. This article will assume knowledge of Express and that an operational Express server is set up with some API endpoints that carry out some logic (check out [this tutorial](https://www.digitalocean.com/community/tutorials/nodejs-express-basics) for some help getting started).

## Goals of Error Handling for RESTful APIs
* **Appropriate status codes are set:** It is important that the HTTP status code is appropriate and as specific as possible with regard to the error that has occurred. Information about what each HTTP status code represents can be found [here](https://developer.mozilla.org/en-US/docs/Web/HTTP/Status). For example, if a GET request for a resource fails because there are no resources corresponding to a provided identifying parameter, a 404 *"Not Found"* status code should be returned. Poor error handling will often be reflected by all error responses setting a  500 *"Internal Server Error* (typically used as generic catch-all status code but should be only set as a last resort).
* **Informative Error Message:** The response body for an erroneous request must include an error message that is insightful, concise and highlighting strictly relevant information (i.e. it should not be populated with garbage). This information will vary on a case-by-case basis, but relevant variables should generally be featured (such as an ID for a resource involved in the thrown error) while avoiding including too many variables such that the message is not readable. Custom error classes may be designed to associate additional metadata with a request without overwhelming the message string.
* **Robust Logging:** Every erroneous request should be logged appropriately. Graceful error handling should ensure that if a developer receives an error response for a request, they should be able to trace the request within the application's log, with at least one entry corresponding to the request error.
* **Consistent Error Format:** The response bodies for erroneous requests must have consistent formatting. That is, an error object returned for a request bound for endpoint A should have the same formatting as an error object for a request bound for endpoint B. This is to ensure that generic error handlers can be designed by clients to handle various error scenarios by assuming the structure of the returned error object.

## Error Handling Middleware
Express defines an interface that can be implemented to create a custom error handling middleware (this will override the primitive default error handler). This middleware function resembles general Express middlewares, although an additional `err` parameter is added to the function header. An example error handling middleware is included below:

***errorHandler.js***
```
const  DEFAULT_STATUS_CODE = 500;

const  errorHandler = (err, req, res, next) => {

	const  status_code = err.status_code || DEFAULT_STATUS_CODE;

	// More advanced logging libraries may be used here instead.
	// This should indicate the location where logging occurs.
	console.log(err);
	
	res.status(status_code).send(
		{
			error:  err.name,
			message:  err.message,
			trace:  err.stack
		}
	);
	next();
}
module.exports = errorHandler;
```
So what does this all mean? This middleware module is intended to be called every time an error is thrown in a request-response flow. It extracts information from the thrown error object, such as status code, error name, message and a stack trace and then prepares a response with an appropriate status code and an informative body. We will show how this data can be passed to the middleware in the [*Custom Error Objects*](#custom-err-objects) section. The middleware function then calls `next()` to ensure that the next express middleware (if one exists) is called.

Now we must ensure that the error handler middleware is used by our Express app.  The example below shows where to include the error handling  middleware in a generic Express server file (i.e. after routers and all other middlewares). The NPM package `express-async-errors` is used to ensure that the middleware handles both syncronous and asyncronous request-response flows (otherwise the handler will only work with syncronous request-response flows). Asyncronous request-response flows are very common in modern backend API development and so it is likely very important to include this in your application. The package can be installed by running `npm install express-async-errors` and more information can be found [here](https://www.npmjs.com/package/express-async-errors).

***server.js***
```
require("express-async-errors");
const  express = require('express');
const  app = express();
const  errorHandler = require('./errorHandler');
const  PORT = process.env.PORT || 5000;

// Other middlewares included here

// Router(s) for express app
require('./routes')(app);

// Include error handler after routes and all other middleware
app.use(errorHandler);

// Finally start server
app.listen(PORT, () => {
	console.log('server is running on port', PORT);
});
```
Great! We have successfully implemented a custom error handling middleware that ensures appropriate status codes are set, all errors are logged and that there is consistent formatting of error responses. ***But how did we get the status code, message and stack trace from the error object in the middleware??*** The answer is custom Error ojects of course.
## Custom Error Objects
Custom error objects can be used to provide additional information via bespoke attributes and methods about an error. This allows us to craft error objects that are unique to the needs of a specific application. In Node.JS, custom error objects are defined by creating a class that extends the generic `Error` class.
### Status Codes
Firstly, we wish to have an easy way of communicating what status code corresponds to the error being thrown. A JS object can be used to map names to these error codes and exported alongside the custom error object. The example includes a subset of HTTP status codes that may be useful for a generic backend API.
```
/** @const  {Object}  [STATUS_CODES] Maps status labels to status codes. */
const  STATUS_CODES = {
	SUCCESS:  200,
	CREATED:  201,
	INVALID:  400,
	UNAUTHORISED:  401,
	FORBIDDEN:  403,
	NOT_FOUND:  404,
	CONFLICT:  409,
	PAYLOAD_TOO_LARGE:  413,
	UNSUPPORTED_MEDIA_TYPE:  415,
	TEAPOT:  418,
	FAILED:  500,
	NOT_IMPLEMENTED:  501,
	INSUFFICIENT_STORAGE:  507
}
```
### Implementing a Custom Error class

Implementing a custom error class is as simple as extending `Error`, calling the parent constructor via `super(message)` in the `CustomError` constructor and then adding any additional attributes and methods as needed. In the below example, we have added a status code attribute which can be passed into the constructor after the error message to associate that error with an appropriate HTTP status code.

***customErrors.js***
```
const STATUS_CODES = { ... } // See above subsection

class CustomError extends Error {

    /**
     * Create a Custom Error.
     * @param {string} [message] A descriptive message for the error.
     * @param {number} [status_code = DEFAULT_STATUS_CODE] The corresponding status code for this error.
     */
    constructor(message, status_code = DEFAULT_STATUS_CODE) {
        super(message);
        this.name = this.constructor.name;
        Error.captureStackTrace(this, this.constructor);
        this._status_code = status_code;
    }

    /**
     * Get the status code for this error.
     * @return {number} The status code for this error.
     */
    get status_code() {
        return this._status_code;
    }

    /**
     * Set the status code for this error.
     * @param {number} [new_status_code] The new status code for this error.
     */
    set status_code(new_status_code) {
        this._status_code = new_status_code;
    }
}

module.exports = {STATUS_CODES, CustomError};
```

### Example Usage
Instead of throwing a generic `Error` object in our API logic, we can now throw our `CustomError` object. In the example below we show how we can throw an informative error for a attempting to get a resource that does not exist.

***routes.js***
```
const db = require('./dbPlugin'); // A plugin for DB requests
const {CustomError, STATUS_CODES} = require('./customErrors');

const routes = (app) => {

    app.get('/resource/:resource_id/', async (req, res) => {

        const resource_id = req.params.resource_id;
        
        try {
            const my_resource = await db.getResource(resource_id);

            if (my_resource == null) {

                // This indicates the requested resource was not found in the DB

                throw new CustomError(
                    `Resource with id=${resource_id} not found`,
                    STATUS_CODES.NOT_FOUND // i.e. 404
                );
            }
            
            res.status(STATUS_CODES.SUCCESS); // Set success status code 200
            res.send(my_resource); // Return resource if it is found

        } catch(err) {
            throw new CustomError(
                `DB Operation Failed: ${err}`,
                STATUS_CODES.FAILED // i.e. 500
            );
        }
    });

};

module.exports = routes;

```

## Conclusion
Congrats! You now know how to implement graceful error handling for your Express application. This guide has provided the scaffolding so that you can tailor your implementation to your applications specific needs. For example, you can add additional attributes to the `Custom Error` class such as the paramaters provided for the request or some metadata about hardware resource consumption etc. Furthermore, you may wish to embed a more advanced logging library into the middleware to provide more detailed logging of error occurences. Be sure to also consider [security and safety concerns](https://expressjs.com/en/advanced/best-practice-security.html) regarding what potentially traceable or identifiable information is logged and at what level. The possibilities are limitless!