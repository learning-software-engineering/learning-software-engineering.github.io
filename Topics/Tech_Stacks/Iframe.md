# Learning Iframe

## Introduction

An iframe is an HTML element used to embed a child website within a parent website. It is supported by most modern browsers, like Chrome, Firefox and Safari.

## Why use Iframe
Sometimes we want to let users interact with a webpage without opening a new webpage tage and redicting to it. For example, we want to embed a survey inside a webpage so that the user can conveniently fill out the survey after reading the previous contents in this webpage.

## How to use Iframes
You can add an iframe element inside your HTML file by following this format:
`<iframe src="some like" title="some title"></iframe>`

There is two important things related to Iframe and I provide instructions about them

### Dynamically resizing an iframe based on content
You can get the scrollhight of the child website by adding a javascript block in the parent html file which contains `X.contentWindow.document.body.scrollHeight + 'px'`;
After getting the scrollheight of the child website, we can delete the scroll bar of the child website and the whole child webpage will be shown inside the parent website without a scrollbar.

### Sending a message from the parent webpage to the child webpage
You can use the `postMessage` API to do this. First, you need to get the iframe element in the parent html file and call `postMessage` with this element. 
Then, you need to add an event listener in the child html file and set the correspond source to the url of the parent website.

## Additional Resources
Here is a link to learning more about iframe if you are interested.
https://www.w3schools.com/tags/tag_iframe.ASP
