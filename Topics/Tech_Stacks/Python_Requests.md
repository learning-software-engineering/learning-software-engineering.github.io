# Python Web Scraping with Requests & BeautifulSoup
In this tutorial, we will go over how to use a combination of the Python libraries [`Requests`](https://pypi.org/project/requests/) and [`BeautifulSoup4`](https://pypi.org/project/beautifulsoup4/) to scrape data from webpages.

## Table of Contents
### [Installation](#installation-1)
### [Basic Usage](#basic-usage-1)
### [Storage](#storage-1)
### [Useful Resources](#useful-resources-1)

## Installation
To start, make sure to install `requests` and `beautifulsoup4`.
```
pip install requests
pip install beautifulsoup4
```

## Basic Usage
### 1. Making Requests
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
After executing the request, you can check the `status_code` of the request. In most cases, a value of `200` indicates success.
```python
if response.status_code == 200:
  # success
```
A full list of HTTP response codes can be found [here](https://developer.mozilla.org/en-US/docs/Web/HTTP/Status).

### 2. Using BeautifulSoup
```python
from bs4 import BeautifulSoup

soup = BeautifulSoup(response.text, 'html.parser')
```
Pass in the content of the response (`response.text`, the raw HTML of the webpage) and indicate the use of an HTML parser to create a new BeautifulSoup object.

We can now make use of the methods `find` and `find_all` to locate specific HTML elements and extract data from them.

#### [find](https://www.crummy.com/software/BeautifulSoup/bs4/doc/#find)
Find and return an element by some of its properties (e.g., tag, id, class, href, etc.).
For example, to locate an anchor element `<a>` with class `title_url`:
```python
element = soup.find('a', class_='title_url')
```
You can then access any of the element's attributes:
```python
element_href = element[href]
element_classes = element[class]
inner_text = element.get_text()
```
You can also use regex to search for matching tags:
```python
import re

# Find the first element with a tag that starts with 'b'
element = soup.find(re.compile('^b'))
```

#### [find_all](https://www.crummy.com/software/BeautifulSoup/bs4/doc/#find_all)
Like `find`, but returns a list of all matching elements.
```python
elements = soup.find_all('li')
for element in elements:
  # Print the inner text of each element
  print(element.get_text())
```

### 3. Using Your Web Browser
To determine which elements to search for, you can the Inspect function on your web browser when visiting the website.
![Inspect Function](https://i.imgur.com/LEyUnK9.png)

For example, using inspect here tells me that the title for each article has tag `h3` and class `gs_rt`:
![Inspect Example](https://i.imgur.com/VTGdiR4.png)

It is important to note that Requests **does not load JavaScript**, so the response given by Requests might be different than what you mgiht expect. To work around this, you can consider alternative libraries such as [`Requests-HTML`](https://pypi.org/project/requests-html/), or disable JavaScript on your web browser (you can use an extension such as [Disable JavaScript](https://chromewebstore.google.com/detail/disable-javascript/jfpdlihdedhlmhlbgooailmfhahieoem) or look for developer tools for your specific browser) to view the webpage that Requests will deliver.

## Storage
With the data extracted, you can store it however you want (e.g., a local csv file, or directly to your database).

## Useful Resources
- [Requests Documentation](https://requests.readthedocs.io/en/latest/)
- [BeautifulSoup4 Documentation](https://www.crummy.com/software/BeautifulSoup/bs4/doc/)
- [HTTP Codes](https://developer.mozilla.org/en-US/docs/Web/HTTP/Status)
- [HTML Syntax](https://www.w3schools.com/html/)
- [Requests Tutorial](https://www.w3schools.com/python/module_requests.asp)
