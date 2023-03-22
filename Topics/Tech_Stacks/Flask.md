# Flask

## Table of contents

### [Prerequisites](#prerequisites-1)

### [Introduction](#introduction-1)

### [Why use Flask?](#why-use-flask-1)

### [Getting Started](#getting-started-1)

### [Resources](#additional-resources)

## Prerequisites

Prior to learning about Flask, you will need basic knowledge regarding the following:

- [Python](https://www.python.org/): Python is a highly popular, high level general purpose programming language. This is essential because Flask is built on Python and is a Python framework.
- [Web Frameworks](https://deepsource.io/glossary/web-framework/): Web frameworks are software frameworks/libraries that help developers write software that runs on the web. Basic knowledge is essential to understanding what Flask provides the user and what to expect from Flask.

## Introduction

Flask is an extremely popular micro web framework, that is written in Python. A micro framework is a framework that has a very low amount of dependencies, thus meaning that it is easy to use and maintain out of the box. However, this may mean that a developer must manually increase the list of dependencies if more features are desired. As a fully functional web framework, Flask provides developers the ability to create complete web applications.

## Why use Flask?

Flask is most commonly compared to Django, which is also a Python web framework. In general, it is a good idea to choose Flask when your application is of relatively smaller size, such as a simple website that serves static web pages. Flask also excels when being used solely as a RESTful web service (for example, for a mobile application).

However, Flask has its limitations: although it is highly flexible, it does not come out of the box with many potentially essential tools, such as form handling, authentication, and dynamic web page handling (though these can be added through adding dependencies). Ultimately, Django is in general better suited for large projects that will be supported in the long term. For a highly in-depth review of Flask vs Django, refer to [this](https://testdriven.io/blog/django-vs-flask/) guide by Michael Herman.

## Getting Started

To install Flask, follow [this](https://flask.palletsprojects.com/en/2.2.x/installation/) guide from the official Flask documentation. To get started in under 10 minutes, follow [this](https://flask.palletsprojects.com/en/2.2.x/quickstart/#a-minimal-application) quickstart hello world application guide (also from the official documentation).

## Additional Resources

### Tutorials

Full-featured Flask blog Youtube tutorial (Corey Schafer) with source code (DB, login Auth, Pagination), recommended as a guide to building a more complex application: [link](https://www.youtube.com/playlist?list=PL-osiE80TeTs4UjLw5MM6OjgkjFeUxCYH)

Very in-depth Flask tutorial with extensive features (login, user interactions, Ajax, forms, Javascript integration), recommended for an in-depth examination of Flask features: [link](https://blog.miguelgrinberg.com/post/the-flask-mega-tutorial-part-i-hello-world)

### Deployment

Flask Heroku deployment guide by GeeksforGeeks: [link](https://www.geeksforgeeks.org/deploy-python-flask-app-on-heroku/)

Flask AWS deployment guide: [link](https://docs.aws.amazon.com/elasticbeanstalk/latest/dg/create-deploy-python-flask.html)

Flask Azure deployment guide: [link](https://learn.microsoft.com/en-us/azure/app-service/quickstart-python?tabs=flask%2Cwindows%2Cazure-cli%2Cvscode-deploy%2Cdeploy-instructions-azportal%2Cterminal-bash%2Cdeploy-instructions-zip-azcli)
