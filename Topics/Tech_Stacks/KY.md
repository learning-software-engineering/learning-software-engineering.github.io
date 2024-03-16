# KY: A versatile HTTP client tool 
## Table of Contents

1. [What is KY](#what-is-ky)
2. [Set up and Installation](#set-up-and-installation)
3. [Usage](#usage)
4. [Request Cancellation](#request-cancellation)
5. [Retries](#retries)
6. [General Benefits](#general-benefits)
7. [Benefits over Regular Fetch](#benefits-over-regular-fetch)
8. [Citation + Useful Links](#some-useful-links)



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
Since KY is a wrapper for flask there is built in support for request cancellations
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

* Lightweight: KY HTTP client is lightweight, with a small footprint, making it suitable for projects where minimizing bundle size is important. "According to Bundlephobia, ky has a minified size of 9.5 KB and a gzipped size of 3.3 KB, while axios has a minified size of 30.5 KB and a gzipped size of 11.7 KB."

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


### All code snippets above as well as benefits are from the following websites
## Some Useful Links:
* [Github Repo for KY](https://github.com/sindresorhus/ky)
* [Official KY Documentation](https://www.npmjs.com/package/ky#kygetinput-options)
* [Example usages of KY](https://snyk.io/advisor/npm-package/ky/example)
* [Medium article going over some benefits of KY](https://medium.com/@muzammilsyed270300/why-you-should-use-ky-instead-of-axios-for-http-requests-in-your-frontend-2c7878be3b30#:~:text=One%20of%20the%20main%20advantages,gzipped%20size%20of%2011.7%20KB)
