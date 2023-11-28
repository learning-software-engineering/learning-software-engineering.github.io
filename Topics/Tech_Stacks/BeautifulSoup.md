# Learning Beautiful Soup



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

# Parse using bs4
soup = BeautifulSoup(response.content, 'html.parser')
```

## Extracting the Data
Once you have parsed the HTML, you can extract data using HTML tags. For example, getting all the paragraphs.

```python
all_p = soup.find_all('p')
```

