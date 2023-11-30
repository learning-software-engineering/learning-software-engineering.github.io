# Learning Beautiful Soup

## Table of Contents
- [Introduction](#introduction)
- [Installation](#installation)
- [Extracting HTML from a Webpage](#extracting-html-from-a-webpage)
- [Parsing using Beautiful Soup](#parsing-using-beautiful-soup)
- [Extracting the Data](#extracting-the-data)
- [When to use Beautiful Soup](#when-to-use-beautiful-soup)
- [Conclusion](#conclusion)

## Introduction
Beautiful Soup is a Python library for parsing HTML and XML documents. It is often used as a tool for web scraping. Beautiful Soup provides a way for users to extract data from web pages. This guide serves as an introduction into using Beautiful Soup 4 for basic web scraping in your Python program. Before starting, you should have a basic understanding of HTML and Python.

## Installation
To use Beautiful Soup, you will also need to install the requests library to fetch the HTML from a website. For Python 3, run the code below.

```bash
pip3 install beautifulsoup4 requests
```

## Extracting HTML from a Webpage
Before using Beautiful Soup, you must get the HTML to parse. If you want to get the HTML from a website, you will need to use the requests library.

```python
import requests

# Get the HTML from the website
url = 'https://example.com'
response = requests.get(url)
```

The resulting response object will contain the HTML source code for the website.

## Parsing using Beautiful Soup
Once you have the HTML, you can use Beautiful Soup to parse the HTML.
```python

import requests
from bs4 import BeautifulSoup

# Get the HTML from the website
url = 'https://example.com'
response = requests.get(url)

# Parse using bs4
soup = BeautifulSoup(response.content, 'html.parser')
```

## Extracting the Data
Once you have parsed the HTML, you can extract data using HTML tags. For example, getting all the paragraphs.

```python
import requests
from bs4 import BeautifulSoup

# Get the HTML from the website
url = 'https://example.com'
response = requests.get(url)

# Parse using bs4
soup = BeautifulSoup(response.content, 'html.parser')

# Find all paragraphs
paragraphs = soup.find_all('p')

# Iterate over paragraphs and store in variable
all_paragraphs = []

for paragraph in paragraphs:
    all_paragraphs.append(paragraph.get_text())
```

## When to use Beatiful Soup
Now that you know how to use Beautiful Soup on a basic level, all you need are the urls for your web scraping program. However, some scraping tasks require more powerful tools. Since Beautiful Soup only parses HTML, it cannot scrape data from dynamically generated content that rely on Javascript. It also cannot automate actions such as clicking buttons to get content. For more complex web pages, refer to the [Selenium web scraping guide.](selenium.md)
