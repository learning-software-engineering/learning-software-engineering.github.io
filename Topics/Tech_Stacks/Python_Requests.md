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

![Google Scholar URL](https://imgur.com/a/ycFWgst)

## Storage

## Useful Resources
