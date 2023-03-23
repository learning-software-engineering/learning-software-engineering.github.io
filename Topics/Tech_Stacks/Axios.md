# Axios: An all-in-one HTTP tool

## What is Axios?

Axios is a JavaScript library that enables developers to send a variety of HTTP requests, performs automatic and contextual serialization of response data, protects
against [XSRF](https://en.wikipedia.org/wiki/Cross-site_request_forgery) attacks, and even allows for request cancellation amongst much more. It can be used in both
the backend and frontend of a full stack application, making it a versatile addition to any JavaScript based application.

## Quick setup and Installation:
If you are using npm the installation command is simply:

```
npm install axios
```

If you are using yarn:

```
yarn add axios
```

Once installed, make sure to include the following at the top of any .js file that makes use of axios:

``` JavaScript
const axios = require('axios');
```

## Examples:
Here are a few examples of common use cases of Axios:

### Sending a GET request and working with it's response (Using Arrow functions):

``` JavaScript
Axios.get("https://www.website.com").then(
(res) => { console.log(res.data); } // This just logs response data but you would do much more 
).catch(
(err) => { console.log(err); } // In the case of an error, we would need to provide some kind of handler
)
```

You can also use regular functions as opposed to Arrow functions, as demonstrated in the next section

### Sending a POST request and working with it's response (Using Regular functions):

``` JavaScript
Axios.post("https://www.website.com", someData).then(
  function(res){
    console.log(res.data);
  }
).catch(
  function(err){
    console.log(err);
  }
)
```
When using Axios.post(), the `someData` parameter could represent any kind of data that needs to be sent in the request body, such as a JSON object.
In addition, `res` is a JSON object that encapsulates the entire response and `err` is a similar JSON object for the error. Usually, `res` has the following attributes:

* `res.status`, the HTTP response code such as 404, 200, 500, etc.
* `res.statusText`, the text of the HTTP response code such as 'OK', 'PAGE NOT FOUND, 'INTERNAL SERVER ERROR', etc.
* `res.data`, the actual information request contained in a JSON format. The format can vary depending on the backend/server response.
* `res.headers`, the headers of the response that usually instruct the browser or receiver to perform a certain protocol/instruction.
* `res.request`, is the is the request that generated this response. It is the last ClientRequest instance in node.js and an XMLHttpRequest instance in the browser.

Along with `.get()` and `.post()`, Axios also supports `.put()`, `.patch()`, `.delete()`, and the entirety of the HTTP request frameworks.

### Using async and await to send form data:

``` JavaScript
await Axios.post('https://website.com', {
    username: 'User1',
    password: '12345'
  }, {
    headers: {
      'Content-Type': 'multipart/form-data'
    }
  }
)
```
Axios also supports `async` and `await` so that we can wait for the necessary data and for the state of the connection to be valid.

## Some Useful Links:
* [Official Axios Documentation](https://axios-http.com/docs/intro)
* [Axios Tutorial](https://www.youtube.com/watch?v=6LyagkoRWYA)
* [Axios GitHub](https://github.com/axios/axios)
* [A thorough article on Axios requests](https://reflectoring.io/tutorial-guide-axios/)
