# BeautifulSoup Guide in Python

## Table of Contents
### [Introduction](#introduction-1)
### [Installation](#installation-1)
### [Set up](#set-up-1)
### [Parsing HTML](#parsing-html-1)
### [Navigating the Parse Tree](#navigating-the-parse-tree-1)
### [Searching the Tree](#searching-the-tree-1)
### [Data Extraction](#data-extraction-1)
### [Additional Resources](#additional-resources-1)

## Introduction

BeautifulSoup is a Python library for parsing HTML and XML documents. It creates parse trees from page source codes 
that can be used to extract data easily. This guide will cover the basics of using BeautifulSoup, along with examples 
and best practices.

For a more comprehensive guide, you can visit the official documentation at 
[Beautiful Soup Documentation](https://www.crummy.com/software/BeautifulSoup/bs4/doc/).

To help you scrape data from a website, please check [this](https://zapier.com/blog/inspect-element-tutorial/)
<img src="https://images.ctfassets.net/lzny33ho1g45/6tl0bR7Iksg9zLxaLYQZKG/5b1f6ae648071253485f5629f0e63ce5/chrome_inspect_element_1.jpg?w=1520&fm=jpg&q=30&fit=thumb&h=760">
## Installation

To use BeautifulSoup, you need to install it along with a parser. The most common parser is `lxml`. You can install 
both using pip:

```bash
pip install beautifulsoup4
pip install lxml
```

#### Using the Built-in `html.parser`:
While `lxml` is known for its speed and efficiency, in some environments, installing external libraries might not be 
feasible. In such cases, you can use Python's built-in `html.parser`. It's slightly slower than lxml but does not require 
any additional installation if you already have Python set up. For `XML` or `XHTML`, `lxml` is highly recommended.

## Set up

To get started with BeautifulSoup, import it along with a request library like requests:

```
from bs4 import BeautifulSoup
import requests
```
## Parsing HTML

You can parse HTML by fetching a web page using requests and passing the content to BeautifulSoup: \
When creating the BeautifulSoup object, you can also specify the parser you want to use: \
- Using `lxml`:
```
url = "http://example.com"
response = requests.get(url)
soup = BeautifulSoup(response.content, 'lxml')
```
- Using `html.parser`:
```
url = "http://example.com"
response = requests.get(url)
soup = BeautifulSoup(response.content, 'html.parser')
```
### Common Pitfalls:

Incorrect URL: Make sure the URL you are trying to scrape is correct and accessible.\
Handling Requests Errors: Be prepared to handle exceptions thrown by the requests library, like `ConnectionError` or 
`HTTPError`.

## Navigating the Parse Tree
### An html parse tree:
<img src="https://i.stack.imgur.com/V2vrr.gif">\
[image source](https://i.stack.imgur.com/V2vrr.gif)

BeautifulSoup allows for easy navigation of the HTML parse tree:

### Accessing Elements Directly

- **Using Tag Names**: Directly access tags as attributes of the BeautifulSoup object.
  ```
  # Sample HTML content
  html_content = '''
  <html>
  <head>
      <title>Example Page</title>
  </head>
  <body>
      <p>Hello World!</p>
  </body>
  </html>
  '''
  
  # Parsing the HTML
  soup = BeautifulSoup(html_content, 'html.parser')
  
  # Accessing the title tag
  
  title = soup.title
  print(title)
  # Expected Output: <title>Example Page</title>
  
  # Accessing the body tag
  body = soup.body
  print(body)
  # Expected Output: <body><p>Hello World!</p></body>
  ```
- **Accessing Children**: Elements in the tree can have children, which are accessed using `.contents` or `.children`.\
Continue with the above code:
  ```
  head_children = soup.head.contents  # List of children under the <head> tag
  print(head_children)
  # Expected Output: [<title>Example Page</title>]
  
  for child in soup.body.children:    # Iterating over children of the <body> tag
      print(child)
  # Expected Output: <p>Hello World!</p>
  ```

### Navigating Using Tag Names

- **Navigating Down**: Tags may contain more tags. These nested tags can be accessed directly.
  ```
  first_paragraph = soup.body.p  # Access the first <p> tag inside <body>
  ```

- **Navigating Up**: Using `.parent`, you can access the parent of a tag.
  ```
  first_paragraph = soup.body.p  # Access the first <p> tag inside <body>
  ```

### Navigating Sideways

- **Navigating Siblings**: Tags at the same level can be navigated using `.next_sibling` or `.previous_sibling`.
  ```
  # Get the next sibling of the first <p> tag
  next_sibling = soup.body.p.next_sibling  
  # Get the previous sibling of the first <p> tag
  prev_sibling = soup.body.p.previous_sibling
  ```
### Navigating Back and Forth

`.next_element` and `.previous_element`: These are used to jump to the next or previous element in the parse tree, not 
just direct siblings.
  ```
  next_element = soup.body.p.next_element  
  # Get the next element in the parse tree after the first <p> tag
  ```
### Common Pitfalls:
- Nonexistent Tags: Always check for a tag's existence before accessing its attributes or contents to avoid 
`AttributeError`.
- Whitespace as Siblings: In HTML, whitespace, including newlines, can be counted as siblings. This can lead to 
unexpected results when navigating siblings.
- Nested Elements: When navigating nested elements, ensure that each parent element exists to avoid `NoneType` errors.

## Searching the Tree
Searching through an `HTML` or `XML` tree is one of the primary functionalities of BeautifulSoup. The library provides 
several methods to locate elements based on their tags, attributes, or text content.

### Using `find()` and `find_all()`

These are two of the most commonly used methods in BeautifulSoup:

- **`find()`**: This method is used to find the first instance of a tag or a tag with specific attributes.
  
  ```
  # Find the first paragraph
  first_paragraph = soup.find('p')

  # Find the first element with a specific class
  first_class_element = soup.find(class_='example_class')
  ```
- **`find_all()`**: This method returns a list of all instances that match the criteria. It's useful for extracting all 
elements of a certain type from a document.
  
  ```
  # Find all links
  all_links = soup.find_all('a')
  
  # Find all elements with a specific class
  all_class_elements = soup.find_all(class_='example_class')
  ```

### Searching by Attributes
You can also search for elements by their attributes
  ```
  # Find elements with a specific ID
  element_with_id = soup.find(id='example_id')
  
  # Find elements with a specific attribute
  elements_with_custom_attr = soup.find_all(attrs={"data-custom": "value"})
  ```
### Searching by Text Content
BeautifulSoup allows you to search for elements based on their text content using the string parameter:
  ```
  # Find element with specific text
  element_with_text = soup.find(string="Example text")
  ```
### Common Pitfalls:
Overlooking Search Methods: Each search method (find, find_all, etc.) has its use case. Choosing the wrong method can 
lead to inefficient scraping.\
Case Sensitivity: Tag and attribute names in searches are case-sensitive. Be mindful of this while searching for tags.

## Data Extraction

### Get Text Method
The `.get_text()` method is used to extract all the text from a document or a specific part of it. This method is 
invaluable when you are interested in the textual content of the HTML elements without any accompanying tags or 
attributes.
```
# Extract text from the entire document
all_text = soup.get_text()
print(all_text)

# Extract text from a specific element
element_text = soup.find('p').get_text()
print(element_text)
```

This method can be fine-tuned by specifying a separator character. For instance, if you want to separate the text of 
different elements with a comma, you can do so by passing a string argument to `get_text()`.
Example with Separator:
```
text_with_separator = soup.get_text(separator=", ")
print(text_with_separator)
```

### Strip Argument
When using .get_text(), you might encounter extra whitespace, which can be removed using the strip argument. This will 
remove leading and trailing whitespaces from the text.
```
clean_text = soup.get_text(strip=True)
print(clean_text)
```

### Extracting Attributes from Tags
In addition to extracting text from HTML elements, BeautifulSoup also allows you to extract attributes from these 
elements. This is particularly useful for scraping data like links (href attributes), image sources (src attributes), 
and other metadata embedded within tags.

#### Basic Approach:

You can access an attribute of an HTML element in the same way you would access a dictionary key in Python
```
# Sample HTML content
html_content = '<a href="https://example.com">Click here!</a>'
soup = BeautifulSoup(html_content, 'html.parser')

# Extracting the 'href' attribute from the first <a> tag
link = soup.find('a')['href']
# you can also use link = soup.find('a').get('href')
print(link)  # Output: https://example.com
```
In this example, `soup.find('a')` locates the first `<a>` tag, and `['href']` directly accesses its href attribute.

#### Handling Multiple Tags:
If your HTML has multiple `<a>` tags and you want to extract href from all of them, you can iterate over the results:

```
# Sample HTML content with multiple <a> tags
html_content = '''
<a href="https://example.com">Link 1</a>
<a href="https://example.org">Link 2</a>
'''

soup = BeautifulSoup(html_content, 'html.parser')

# Extracting 'href' attributes from all <a> tags
for link in soup.find_all('a'):
    print(link.get('href'))
```

In this case, `soup.find_all('a')` fetches all `<a>` tags, and `link.get('href')` is used to safely extract the href 
attribute. Using `.get()` is safer because it returns None if the attribute doesn't exist, avoiding a KeyError.

#### Extracting Multiple Attributes:
In cases where you need to extract more than one attribute from an element, you can iterate over the element's 
attributes:

```
# Extracting all attributes of the first anchor tag
html_content = '''
<a href="https://example.com" id="main_content">Link 1</a>
'''
soup = BeautifulSoup(html_content, 'html.parser')
anchor_tag = soup.find('a')
for attribute, value in anchor_tag.attrs.items():
    print(f"{attribute}: {value}")
```
This will print out all attributes and their values for the specified element.

## Additional Resources
Please look at `HTML_Guide.md` for reference to html content.

More tutorials/resources on BeautifulSoup:\
https://realpython.com/beautiful-soup-web-scraper-python/ \
https://github.com/wention/BeautifulSoup4 \
https://www.geeksforgeeks.org/implementing-web-scraping-python-beautiful-soup/ \
https://www.tutorialspoint.com/beautiful_soup/index.htm

How to navigate a website by inspecting:\
https://zapier.com/blog/inspect-element-tutorial/ \
https://blog.hubspot.com/website/how-to-inspect
