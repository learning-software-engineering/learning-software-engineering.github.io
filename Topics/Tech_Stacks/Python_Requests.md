# Python Web Scraping with Requests
In this tutorial, we will go over how to use  the Python library [`Requests`](https://pypi.org/project/requests/) to retrieve content from web pages for scraping.

## Table of Contents
### [Installation](#installation-1)
### [Basic Usage](#basic-usage-1)
### [Parsing](#parsing-1)
### [Useful Resources](#useful-resources-1)

## Installation
To start, install `requests`.
```
pip install requests
```

## Basic Usage
Make sure to import requests.
```python
import requests
```

### GET
Most webpages can be scraped/retrieved using the GET method. This is analogous to sending a HTTP GET request.
```python
response = requests.get(url, params=params)
```
To determine the parameters needed, you can visit the website using your web broswer and then examine the end of the URL after the question mark.

For example, the parameters needed for Google Scholar are the language `hl` and the query `q`.

![Google Scholar URL](https://i.imgur.com/bOZUgYf.png)

These parameters can then be included in a dctionary.
```python
params = {
  'hl': 'en',     # Set the language to English
  'q': 'python',  # Keyword to search
}
```
You can then retrieve the content of the webpage, which in most cases is the HTML of the webpage.
```python
content = response.text
```

### POST
Some endpoints may use a HTML Form or a JSON object to set the necessary parameters to display the data that you need. In ths case, you can use the `POST` method.
```python
data = {
  'key': 'value'
}

# Send data as HTML form
response = requests.post(url, data=data)

# Send data as JSON
response = requests.post(url, json=data)
```
You can then utilize `response` in the same way as `GET`.

To determine the data that you need to send, you can use the Network tab in your browser's developer tools to examine the specific `POST` request that website sends.

### Sessions
Alternatively, you can use `SESSIONS` when making multiple requests to the same webpage, or if you want to persist cookies or other information like headers between requests. The syntax is largely the same with the exception of creating and using a session for making requests.
```python
session = requests.Session()
response1 = session.post(url)
response2 = session.get(url)
```

### Status Code
After executing the request, you can check the `status_code` of the request. In most cases, a value of `200` indicates success.
```python
if response.status_code == 200:
  # success
```
A full list of HTTP response codes can be found [here](https://developer.mozilla.org/en-US/docs/Web/HTTP/Status).

## Parsing
With the webpage retrieved, you can now parse the data using a library such as [BeautifulSoup4](https://pypi.org/project/beautifulsoup4/).

## JavaScript
It is important to note that Requests **does not load JavaScript**, so the response given by Requests might be different than what you mgiht expect. To work around this, you can consider alternative libraries such as [`Requests-HTML`](https://pypi.org/project/requests-html/), or disable JavaScript on your web browser (you can use an extension such as [Disable JavaScript](https://chromewebstore.google.com/detail/disable-javascript/jfpdlihdedhlmhlbgooailmfhahieoem) or use developer tools in your specific browser) to view the webpage that Requests will deliver.

## Useful Resources
- [Requests Documentation](https://requests.readthedocs.io/en/latest/)
- [HTTP Codes](https://developer.mozilla.org/en-US/docs/Web/HTTP/Status)
- [HTML Syntax](https://www.w3schools.com/html/)
- [Requests Tutorial](https://www.w3schools.com/python/module_requests.asp)
