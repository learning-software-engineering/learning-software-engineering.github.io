# Asynchronous External API Interface in a Python Application

## Table of Contents
1. [Introduction](#introduction)
2. [What is an API?](#what-is-an-api)
3. [What does 'Asynchronous' mean?](#what-does-asynchronous-mean)
4. [Installation](#installation)
5. [Types of Requests](#types-of-requests)
   - [GET Request](#get-request)
   - [POST Request](#post-request)
   - [PUT Request](#put-request)
   - [DELETE Request](#delete-request)
6. [Introduction to Sending Requests](#introduction-to-sending-requests)
   - [Session configuration](#session-configuration)
   - [Sending the request](#sending-the-request)
7. [Asynchronous Requests](#asynchronous-requests)
   - [Asynchronous request execution](#asynchronous-request-execution)
   - [The `asyncio` library](#the-asyncio-library)
   - [Using `with`](#using-with)
8. [A Note on API Tokens](#a-note-on-api-tokens)

9. [Designing an Interface: Case Study](#designing-an-interface-case-study)
   - [Class initialization and API token configuration](#class-initialization-and-api-token-configuration)
   - [Checking connection status](#checking-connection-status)
   - [Retrieving flows](#retrieving-flows)
   - [Interface basics](#interface-basics)
10. [Evolving Your Interface: Case Study](#evolving-your-interface-case-study)
    - [Interface initialization and API token configuration](#interface-initialization-and-api-token-configuration)
    - [Interface utilities](#interface-utilities)
    - [Sending requests](#sending-requests)
    - [Separating requests into use-cases](#separating-requests-into-use-cases)
11. [`httpx` Error Handling](#httpx-error-handling)
12. [Conclusion](#conclusion)


## Introduction

This tutorial will explore how to set up an asynchronous interface with an external API in a Python-based server, in which responsiveness and scalability are crucial.

## What is an API?

An API, or Application Programming Interface, is an access point and specification-set allows one software application to interact with another. It defines the methods and data formats that applications can use to request and accept information.

APIs are typically accessed via the use of a API Token or API Key. This is a string of characters that identifies the user, generally for the API provider to provide access to the specific user's data, track usage, and limit potential bad actors' excessive use of the API by restricting the number of requests that can be made using the token in an internal of time.

## What does 'Asynchronous' mean?

In traditional synchronous programming, tasks are executed sequentially, one after the other. Asynchronous programming, on the other hand, a program can perform tasks concurrently without waiting for each task to complete before starting the next one, improving overall efficiency and responsiveness.

To illustrate this difference, consider a web server that must accomodate many end-users:

Synchronous Approach:

In a synchronous implementation, the server would handle one request at a time. When a client sends a request, the server then processes it when received, and while processing it cannot handle other requests. If the server encounters a blocking operation (such as reading from a file or making a network request), it would wait until that operation is completed before moving on to processing the next request. This approach has the benefit of simplicity, but suffers from inefficiency when waiting for operations to be completed. This however may be acceptable depending on the use case (such as if it is oriented for single-user use).

Asynchronous Approach:

In an asynchronous implementation, the server can start processing a request and, instead of waiting for time-consuming operations (like reading from a file or making a network request) to complete, it can move on to handle another request. This is well-suited for I/O tasks - where the program spends time waiting for external operations to complete - where being asynchronous improves server responsiveness.

## Installation

Please ensure you have installed a version of Python 3 on your computer (a version of Python 3.7 or later is advised). Additionally, you will need to install the `httpx` library - providing an HTTP client for Python with support for asynchronicity. Run the following `pip` command in a terminal to install it:

```bash
pip install httpx
```

## Types of Requests

HTTP supports a variety of types of requests, each delineating a different purpose, and the choice of which one to use depends on the operation you want to perform via the external API. The most common request types are:

### GET Request

The GET request is used to retrieve data from the API, without any changes known to be made to data or state on the API server itself.

### POST Request
The POST request is used to submit data to modify a specific resource on the external server.

### PUT Request
The PUT request is used to create or overrite a resource on the external server.

### DELETE Request
The DELETE request is used to request that a resource be removed or deleted on the external server.


## Introduction to Sending Requests

Let us begin by first looking at a basic example of synchronously sending a request to an API using Python. We will use the `requests` library for this motivating example, which you may install using ```pip install requests``` (though this is unnecessary unless you wish to follow along).

For the purpose of demonstration, we will be looking at the API for the website https://app.rapidpro.io/ to serve as a generic example of common API formatting. Please see [this page](https://app.rapidpro.io/api/v2/flows) to learn more about the format of the requests we are about to make.

```python
import requests

# session configuration
token = '1k2ej1kjek1usj1us1s1ous'
session = requests.Session()
session.headers.update({'Authorization': f'Token {token}'})

# send request
response = self.session.get(url='https://app.rapidpro.io/api/v2/flows.json',
                            params={'uuid': '2313-0293-8732'})

data = response.json()
print(data)

```

In this example, we are using the `requests` library as discussed to send a synchronous HTTP GET request to an API endpoint. Let's break down the key components of this motivating example:

### Session configuration

Before sending the request, we set up a session configuration. `Session` in the `requests` library allow you to persist certain parameters across multiple requests by using the same initialized `Session`. We set up a `Session` with an Authorization header containing an access token. This header format was specified in the instructions for this API we are using in order to authenticate requests.

```python
token = '1k2ej1kjek1usj1us1s1ous'
session = requests.Session()
session.headers.update({'Authorization': f'Token {token}'})
```

Here, `token` stores our API token, and we create a session with these necessary headers for authentication.

### Sending the request

The `get` method of the session object is then used to send a GET request to a specified URL (`'https://app.rapidpro.io/api/v2/flows.json'`). Query parameters - in this case, the `uuid` parameter, the ID of the resource to be retrieved - can be included in the request using the `params` argument via a Python dictionary.

```python
response = session.get(url='https://app.rapidpro.io/api/v2/flows.json',
                        params={'uuid': '2313-0293-8732'})
```

The `response` variable now contains the server's response to our request, and we extract the JSON data from the response for further use by converting to to Python dictionary:

```python
data = response.json()

# or by using the built-in json library:
import json
data = json.loads(response.text)
```

If you wish to see what the content of this response may look like, please see the response section [on this page](https://app.rapidpro.io/api/v2/flows). In general however, it will be in some format alike to a Python dictionary, like this:

```python
# Sample response to a API endpoint to get an attendence list of student names
{
    "results": ['Keanu Smith', 'Sarah Smith', 'Jimmy Woo']
}
```

## Asynchronous Requests

Now, let's adapt this example to be asynchronous using `httpx` and the Python built-in library `asyncio`. Before we proceed, again please ensure you have installed the `httpx` library for Python:

```bash
pip install httpx
```

In this asynchronous implementation, the code structure must change to accommodate the asynchronous nature of the request. We will use the `httpx.AsyncClient` for asynchronous communication:

```python
import httpx
import asyncio

async def make_async_request():
    token = '1k2ej1kjek1usj1us1s1ous'
    client = httpx.AsyncClient()
    client.headers.update({'Authorization': f'Token {token}'})
    
    params = {'uuid': uuid}
    response = await client.get('https://app.rapidpro.io/api/v2/flows.json',  
                                params=params)
    data = response.json()
    print(data)

# Run the function in an asyncio event loop
asyncio.run(make_async_request())
```

As you can see, `httpx` works very similarly to the `requests` library, with `httpx.AsyncClient` taking the place of `requests.Session`. 

### Asynchronous request execution
The `async` and `await` keywords are introduced to make the request asynchronously. This ensures that the execution of the function is not blocked, allowing other asynchronous tasks to be processed while waiting for the API response. 

The function in which the request is made is defined using the `async` keyword. Once the asynchronous request is made, we `await` the response and process it accordingly. We can then extract the JSON data from the response for further use (provided the request was successful).

### The `asyncio` library
`asyncio` is a Python built-in library that provides functionality for asynchronous programs. As this function defined here `make_async_request` is tagged as `async`, when it is called it must be called in an asynchronous fashion, such as:
```python
async make_async_request()
```

However, sometimes this is not feasible, such as when we are calling this function as part of the main execution of this Python program. In such cases, we can make use of `asyncio.run`, which allows us to call an asynchronus function without requiring the caller to be asynchronous as well.

Note: `asyncio.run` cannot be used within a function that is itself `async`. If this is done, an exception will be raised.

### Using `with`
Although with the `requests` library we were able to re-use the same `Session` to send multiple requests, this is not as feasible with `httpx.AsyncClient`. `AsyncClient` does provide this functionality, but due to its asynchronous nature one may encounter exceptions arising from trying to use an already in-use file descriptor. 

It is recommended to re-create the `AsyncClient` before sending another request to avoid this issue. This is made all-the-easier using the `with` keyword that initializes the client as a local variable, which is then deleted once outside of the scope of the `with`:

```python
import httpx
import asyncio

async def make_async_request():
    token = '1k2ej1kjek1usj1us1s1ous'
    async with httpx.AsyncClient() as client:
        client.headers.update({'Authorization': f'Token {token}'})
        
        endpoint = 'https://app.rapidpro.io/api/v2/flows.json'
        params = {'uuid': uuid}
        response = await client.get(url=endpoint, 
                                    params=params)
        data = response.json()
        print(data)

# Run the function in an asyncio event loop
asyncio.run(make_async_request())
```

## A Note on API Tokens

Storing an API token as done in the examples above is not the correct approach from a security standpoint. Instead, a more sound solution is to make use of environment variables, such as below:

```python
import os

token = os.environ.get('API_TOKEN')
```

Or secure storage in a database (such as if each user of the application has their own API token).


## Designing an Interface: Case Study
Now that we have discussed the implementation of handling API requests and responses, we must now discuss how to integrate this into a Python-based application.

```python
import httpx


class RapidProAPI:
    def __init__(self, token: str):
        ...

    def set_api_token(self, token: str):
        ...

    async def get_connection_status(self):
        ...

    async def get_flows(self, uuid: str = '', before_date: str = '', after_date: str = ''):
       ...

```

As you can see, here we have an outline of a class that handles API requests. We have implemented a Python class, `RapidProAPI`, designed to interact with the RapidPro API. This class encapsulates methods for setting the API token, retrieving flows, and checking the validity of the configured API token. Let's take a closer look at this implementation.

### Class initialization and API token configuration

In the constructor (`__init__`), the class is initialized with the specified API token. The `set_api_token` method is provided for later updating the API token to be used in subsequent requests.

```python
def __init__(self, token: str):
    self._token = token
    self.API_URL = "https://app.rapidpro.io/api/v2/"

def set_api_token(self, token: str):
    self._token = token
```

### Checking connection status

The `get_connection_status` method checks whether the configured RapidPro API token is valid by making a request to the API root.

```python
async def get_connection_status(self):
    async with httpx.AsyncClient() as client:
        client.headers.update({'Authorization': f'Token {self._token}'.strip()})
        response = await client.get(url=f'{self.API_URL}')
    return response
```

### Retrieving flows

The `get_flows` method retrieves flows from the RapidPro API based on specified parameters ID and date range.

```python
async def get_flows(self, uuid: str = '', before_date: str = '', after_date: str = ''):
    async with httpx.AsyncClient() as client:
        client.headers.update({'Authorization': f'Token {self._token}'})
        response = await client.get(url=f'{self.API_URL}flows.json',
                                    params={'uuid': uuid,
                                            'before': before_date,
                                            'after': after_date})
    return response
```

### Interface basics

This class provides a structured and modular way to interact with the RapidPro API. As we can see, it sends the request specified and returns the response from the external API. These are the basics for an interface, but a good implementation should go further than this.

## Evolving Your Interface: Case Study
With this class created to handle the sending of requests and return of responses asynchronously, we can now focus on adding functionality to our interface. This can be done by creating another class that makes use of the prior class. Here is the outline of one such class:

```python
import json
from asyncio import run


class RapidProInterface:
    """
    Interface for using RapidPro API.
    """
    def __init__(self, token: str = ""):
        ...

    def set_api_token(self, token: str):
        ...

    def validate_token(self):
        ...

    def get_flow(self, uuid: str):
        ...

    def get_flows(self, before_date: str = '', after_date: str = ''):
        ...

    @staticmethod
    def get_status_code_interpretation(status_code: int):
        ...

    class AbstractRequestException(Exception):
        ...

    class ResponseParsingException(AbstractRequestException):
        pass

    class RequestFailureException(AbstractRequestException):
        pass

    class TokenValidationException(AbstractRequestException):
        pass
```

Let's break down the design and functionality of this implementation:

### Interface initialization and API token configuration

In the constructor (`__init__`), the class is initialized and creates an instance of our API-handler class using the provided token. The `set_api_token` method makes use of the API-handler class' method to update the API token to be used.

```python
def __init__(self, token: str = ""):
        self.rapidProAPI = RapidProAPI(token)

def set_api_token(self, token: str):
    self.rapidProAPI.set_api_token(token)
```

### Interface utilities
Our API-handler class simply returned any response it would receive. However, not all responses contain the expected information. It is important to read the API's documentation to learn more about what status codes may be returned in a response, and how to interpret them.

Our Interface has the method `get_status_code_interpretation` that - using the breakdown of status codes in the API documentation - maps a status code to its meaning (to provide additional information). We can retrieve a status code from a request response via `request.status_code`.
```python
@staticmethod
def get_status_code_interpretation(status_code: int):
    match status_code:
        case 200:
            return "200: Request was successful."
        case 201:
            return "201: Resource was successfully created."
        case 204:
            return "204: Successful DELETE or POST request that updated multiple resources."
        case 400:
            return ("400: Request failed due to invalid parameters. "
                    "Do not retry with the same values. "
                    "The body of the response contains further information.")
        case 403:
            return "403: You do not have permission to access this resource."
        case 404:
            return "404: The specified resource was not found."
        case 429:
            return ("429: You have exceeded the rate limit for this endpoint (of 2,500 requests per hour). "
                    "See 'Retry-After' in response header for seconds-count until requests replenish.")
        case _:
            return f"{status_code}: Unknown status code."
```

In combination with this, we have defined class-specific exceptions that can be used to catch and handle any raised exceptions:

```python
    class AbstractRequestException(Exception):
        def __init__(self, message: str, response: httpx.Response):
            super().__init__({
                "message": message,
                "response": response})
            self.status_code = response.status_code
            self.message = message

    class ResponseParsingException(AbstractRequestException):
        pass

    class RequestFailureException(AbstractRequestException):
        pass

    class TokenValidationException(AbstractRequestException):
        pass
```

The `message` that is stored in these exceptions is the one retrived from `get_status_code_interpretation`.

With these utilities, we can now look at how requests can be sent using this new interface class.

### Sending requests

The `get_connection_status` method checks whether the configured RapidPro API token is valid by making a request to the API root via use of the API-handler class:

```python
def validate_token(self):
    response = run(self.rapidProAPI.get_connection_status())
    if response.is_success:
        return True
    elif response.status_code == 403:
        return False
    else:
        raise self.TokenValidationException(self.get_status_code_interpretation(response.status_code),
                                            response)
```

As we can see, we use the `asyncio.run` function to do these requests as the RapidProAPI class had asynchronous methods, but the RapidProInterface class does not (for ease of use). 

Once the response is returned, it is determined whether the connection was a success and a boolean is returned whether it was or was not based on the status code. Otherwise, an error must be raised with the appropriate interpretation of the abnormal status code.

### Separating requests into use-cases
Now, we will take a look at the extension of the GET request for a flow that we examined earlier. In this new interface class, we can partition the functionality of this GET request for better usability: into `get_flow(uuid)` and `get_flows(before_date, after_date)`.

```python
def get_flow(self, uuid: str):
    response = run(self.rapidProAPI.get_flows(uuid=uuid))
    if response.is_success:
        try:
            response_dict = json.loads(response.text)
            returned_flows = response_dict.get('results')
            if returned_flows:
                return returned_flows[0]
            else:
                return None  # no flows match this UUID
        except json.decoder.JSONDecodeError:
            raise self.ResponseParsingException("Failed to parse flow in HTTP response.", response)
    else:
        raise self.RequestFailureException(self.get_status_code_interpretation(response.status_code), response)


def get_flows(self, before_date: str = '', after_date: str = ''):
    response = run(self.rapidProAPI.get_flows(before_date=before_date, after_date=after_date))
    if response.is_success:
        try:
            response_dict = json.loads(response.text)
            returned_flows = response_dict.get('results')

            if returned_flows is not None:
                return returned_flows
            else:
                return []
        except json.decoder.JSONDecodeError:
            raise self.ResponseParsingException("Failed to parse flow in HTTP response.", response)
    else:
        raise self.RequestFailureException(self.get_status_code_interpretation(response.status_code), response)
```

As we can see, this partition into two separate methods allows us to parse the responses differently. In `get_flow`, the ID of the requested resource is a parameter, meaning that only one resource is expected to be retrieved, and the response is parsed as such. In `get_flows`, all resources within a date range are requested, so the response is instead parsed as an array of resources.

## `httpx` Error Handling

A well-encapsulated API Interface will effectively catch any exceptions raised by the `httpx.AsyncClient`. There are a plethora of exceptions provided by the `httpx` library that can be caught if raised. [A full list of these exceptions can be seen here.](https://www.python-httpx.org/exceptions/)

We can improve the example `get_connection_status` method by making use of these:

```python
async def get_connection_status(self):
    async with httpx.AsyncClient() as client:
        client.headers.update({'Authorization': f'Token {self._token}'.strip()})
        try:
            response = await client.get(url=f'{self.API_URL}',
                                        timeout=2)
        except httpx.TimeoutException as e:
            ... # your error-handling code; could choose to resend or raise an error
    return response
```

As we can see, we have introduced a timeout of 2 seconds in this GET request (`httpx` sets timeout to 6 seconds by default), and if this timeout is reached we will catch and handle the raised exception.

There are many more exceptions that may be handled individually, or the superclass of these exceptions `httpx.HTTPError` may be caught to handle all of them.

## Conclusion

Congratulations! You've successfully learned how to set up an asynchronous interface with an external API in a Python-based application using `asyncio` and `httpx`. Using this example that we've stepped through together, you are prepared to implement your own External API interface for any API your project needs.

To further enhance your knowledge, consider exploring the official documentation for [httpx](https://www.python-httpx.org/) and [asyncio](https://docs.python.org/3/library/asyncio.html).

Good luck in your future endeavours!
