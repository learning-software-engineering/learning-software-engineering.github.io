# Python Web Scraping with Requests & BeautifulSoup

## Table of Contents
### [Introduction](#introduction-1)
### [Basic Usage](#basic-usage-1)
### [Storage](#storage-1)
### [Useful Resources](#useful-resources-1)

## Introduction
In this tutorial, we will go over how to use a combination of the Python libraries [requests](https://requests.readthedocs.io/en/latest/) and [BeautifulSoup4](https://www.crummy.com/software/BeautifulSoup/bs4/doc/) to scrape data from webpages.

To start, install requests and bs4.
```
pip install requests
pip install beautifulsoup4
```

## Basic Usage
### Making Requests
Most webpages can be scraped/retrieved using the GET method. This is analogous to sending a HTTP GET request.
```python
import requests

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
After executign the request, you can check the `status_code` of the request to determine its success. A value of `200` indicates success.
```python
if response.status_code != 200:
  # failure
```
A full list of HTTP response codes can be found [here](https://developer.mozilla.org/en-US/docs/Web/HTTP/Status).

### Using BeautifulSoup
```python
from bs4 import BeautifulSoup

soup = BeautifulSoup(response.text, 'html.parser')
```

## Storage

## Useful Resources
