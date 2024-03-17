# KY: A versatile HTTP client tool 
## Table of Contents

1. [What is KY](#what-is-ky)
2. [Set up and Installation](#set-up-and-installation)
3. [Usage](#usage)
4. [Request Cancellation](#request-cancellation)
5. [Retries](#retries)
6. [General Benefits](#general-benefits)
7. [Benefits over Regular Fetch](#benefits-over-regular-fetch)
8. [Common Network Errors](#common-network-errors)
9. [Citation + Useful Links](#some-useful-links)



## What is KY:
KY HTTP client is a lightweight JavaScript library for making HTTP requests in web applications. It is a wrapper on the Fetch API, a contemporary interface for network-based asynchronous resource fetching. KY HTTP client offers a straightforward and user-friendly API along with capabilities like request cancellation, retries, and automatic JSON parsing in an effort to streamline the process of sending HTTP requests.

## Set up and installation 
To download using npm run the following command

```
npm install ky
```
After installation is complete make sure to add the following line at the top of any document requiring ky
```
import ky from 'ky'
```
## Usage
```
const json = await ky.post('https://example.com', {json: {foo: true}}).json();
```

# Get
```
const apiUrl = 'https://api.example.com/data';

ky.get(apiUrl)
  .then(response => {
    if (response.ok) {
      return response.json();
    } else {
      throw new Error(`HTTP error! Status: ${response.status}`);
    }
  })
  .then(data => {
    console.log('Data received:', data);
  })
  .catch(error => {
    console.error('Error:', error);
  });
```

# Post
```
const apiUrl = 'https://api.example.com/data';

// Data to send
const postData = {
  name: 'Shaffaan Bin Aamir',
  message: 'Hello if you are reading this you are maybe in CSC301!'
};

ky.post(apiUrl, {
  json: postData
})
  .then(response => {
    // Response is successful (status code 200-299)
    if (response.ok) {
      return response.json();
    } else {
      throw new Error(`HTTP error! Status: ${response.status}`);
    }
  })
  .then(data => {
    console.log('Response:', data);
  })
  .catch(error => {
    console.error('Error:', error);
  });
```

# Request Cancellation 
Since KY is a wrapper for fetchAPI there is built in support for request cancellations
This can be done using the AbortController
```
Following code is from KY documentation. Link provided at the end of the document

const controller = new AbortController();
const {signal} = controller;

setTimeout(() => {
	controller.abort();
}, 5000);

try {
	console.log(await ky(url, {signal}).text());
} catch (error) {
	if (error.name === 'AbortError') {
		console.log('Fetch aborted');
	} else {
		console.error('Fetch error:', error);
	}
}
```

# Retries 
```
const json = await ky('https://example.com', {
	retry: {
		limit: 10,
		methods: ['get'],
		statusCodes: [413],
		backoffLimit: 3000
	}
}).json();
```
Implementing HTTP retry mechanisms in scenarios with spotty network conditions can significantly enhance the reliability and availability of distributed systems. By automatically retrying failed requests, applications can mitigate the impact of transient network issues, reducing service disruptions and improving overall user experience. For example, in a mobile application where users may experience intermittent connectivity while traveling, HTTP retries can help ensure that critical requests, such as fetching messages or updating data, are eventually successful despite temporary network outages. This approach minimizes user frustration and maintains seamless functionality, ultimately increasing user satisfaction and retention.


## General Benefits
Some of the benefits KY provides are 

* Lightweight: KY HTTP client is lightweight, with a small footprint, making it suitable for projects where minimizing bundle size is important. "According to Bundlephobia, ky has a minified size of 9.5 KB and a gzipped size of 3.3 KB, while axios has a minified size of 30.5 KB and a gzipped size of 11.7 KB." [Medium article going over some benefits of KY](https://medium.com/@muzammilsyed270300/why-you-should-use-ky-instead-of-axios-for-http-requests-in-your-frontend-2c7878be3b30#:~:text=One%20of%20the%20main%20advantages,gzipped%20size%20of%2011.7%20KB)

* Promise-based API: It provides a simple and intuitive Promise-based API for making HTTP requests, making it easy to handle asynchronous operations and manage response data.

* Automatic JSON parsing: It automatically parses JSON responses, reducing boilerplate code for handling JSON data from API endpoints. This is especially useful if alot of requests are being made in the same file and code is becoming convoluted 

* Request cancellation: KY HTTP client supports request cancellation, allowing you to cancel pending requests, which can be useful for scenarios like user navigation or when a request is no longer needed.

* Retries: It supports automatic retries for failed requests, enhancing reliability in unstable network conditions.

* Interceptors: KY HTTP client provides interceptors, enabling you to modify requests or responses globally, such as adding headers or logging, which can streamline request/response processing.

* Modular: KY HTTP client is modular, allowing you to use only the features you need, which can help keep the codebase clean and efficient.

* Ky offers support for multiple functions within the hooks.beforeRequest option, enabling sequential execution before the request is dispatched. This functionality facilitates various modifications or actions based on the request. For instance, you can incorporate a function to log request details and another to append a custom header. Additionally, async functions can be utilized within these hooks, allowing them to await promise resolution before advancing to the subsequent hook or request. Conversely, Axios also allows multiple functions in the interceptors.request option, but they execute in reverse order, potentially leading to confusion.


## Benefits over regular Fetch
* Simpler API
* Method shortcuts (ky.post())
* Treats non-2xx status codes as errors (after redirects)
* Retries failed requests
* JSON option
* Timeout support
* URL prefix option
* Instances with custom defaults
* Hooks

The above benefits copied from the KY documentation. Link is present below

## Common Network Errors
Because of the fact that KY is an HTTP client alot of errors that users usually run in are network errors. I have included a list of common network errors that one may encounter. I have also linked an article that goes in detail about what each error means and how to solve them. Furthermore the KY repo has alot of issues and their solutions are regularly posted. I have linked the repo below

* 400 Bad Request: The server cannot process the request due to invalid syntax.
* 401 Unauthorized: The request requires user authentication.
* 403 Forbidden: The server understood the request, but refuses to authorize it.
* 404 Not Found: The server cannot find the requested resource.
* 408 Request Timeout: The server timed out waiting for the request.
* 429 Too Many Requests: The user has sent too many requests in a given amount of time.
* 500 Internal Server Error: The server encountered an unexpected condition that prevented it from fulfilling the request.
* 502 Bad Gateway: The server received an invalid response from the upstream server.
* 503 Service Unavailable: The server is currently unable to handle the request due to temporary overloading or maintenance of the server.
* 504 Gateway Timeout: The server was acting as a gateway or proxy and did not receive a timely response from the upstream server.
* DNS Server Not Found: The DNS server used by your computer or network connection cannot be reached.
* Connection Refused: The connection attempt was refused by the remote server.
* Connection Reset: The connection was forcibly closed by the peer.

  
[Common API erros and how handle them](https://technologyadvice.com/blog/information-technology/api-error/)
[Detecting Network Failures with fetch](https://medium.com/to-err-is-aaron/detect-network-failures-when-using-fetch-40a53d56e36)

## CORS Error and how to handle it with KY
A CORS error, or Cross-Origin Resource Sharing error, occurs when a web application tries to make a request to a resource (like an API) that resides on a different domain, protocol, or port than the one from which the initial web page was served. [CORS docs](https://developer.mozilla.org/en-US/docs/Web/HTTP/CORS/Errors)
There are many different CORS error and ways of handling them .This article I have linked goes in detail about how to solve them.
[CORS trouble shooting](https://www.linkedin.com/pulse/its-always-cors-problem-troubleshooting-solving-errors-carrubba-/)

A very popular method is using a CORS proxy service to bypass CORS restrictions. Ky allows you to easily configure a custom fetch handler, so you can integrate a CORS proxy with Ky.

```
import ky from 'ky';

const proxyUrl = 'https://cors-anywhere.herokuapp.com/';
const apiUrl = 'https://example.com/api/data';
// Make a GET request through the CORS proxy
ky.get(proxyUrl + apiUrl).then(response => {
}).catch(error => {
});
```


### All code snippets above as well as benefits are from the following websites aswell as the links provided above
## Some Useful Links:
* [Github Repo for KY](https://github.com/sindresorhus/ky)
* [Official KY Documentation](https://www.npmjs.com/package/ky#kygetinput-options)
* [Example usages of KY](https://snyk.io/advisor/npm-package/ky/example)
* [Medium article going over some benefits of KY](https://medium.com/@muzammilsyed270300/why-you-should-use-ky-instead-of-axios-for-http-requests-in-your-frontend-2c7878be3b30#:~:text=One%20of%20the%20main%20advantages,gzipped%20size%20of%2011.7%20KB)
