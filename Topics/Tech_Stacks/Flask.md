# Intro to Flask with Flask-SQLAlchemy


## 1. Introduction
###  What is Flask and why is it useful?
Flask is a lightweight and flexible web framework for Python. Developed by Armin Ronacher, it is designed to be simple and easy to use, providing the essentials for building web applications without imposing rigid structures. Flask is often referred to as a "micro" framework because it focuses on keeping the core simple and extensible, allowing developers to choose the tools and libraries they need. 

The inclusion of the Jinja2 templating engine, built-in development server and Flask's native support for RESTful request handling are desirable features. Its versatility in deployment and suitability for prototyping and small to medium-sized projects make Flask an ideal framework for projects where customization and control over the stack are key considerations.

Here is an overview of Flask: [Flask Overview](https://flask.palletsprojects.com/en/3.0.x/#)

### What is Flask-SQLAlchemy and why is it useful?

Flask-SQLAlchemy is an extension for Flask that integrates SQLAlchemy, a powerful SQL toolkit and Object-Relational Mapping (ORM) library, into Flask applications. This extension simplifies database interactions by providing a convenient interface for defining models, executing queries, and managing database connections seamlessly within the Flask framework.

Some of the advantageous features include seamless integration with Flask, session handling, support for Flask Script and Flask Restful, compatibility with Flask extensions and database migrations.



## 2. Getting set up
### Setting up Flask:
First install Flask following the instructions here: [Flask installation](https://flask.palletsprojects.com/en/3.0.x/installation/)

This will make sure that all dependencies are obtained, the virtual environment is created and Flask is installed.

Next, the Flask application can be set up. 
This shows you how the project layout works: [Project Layout](https://flask.palletsprojects.com/en/3.0.x/tutorial/layout/)

And this is how to set the application up:[Application Setup](https://flask.palletsprojects.com/en/3.0.x/tutorial/factory/)

Alternatively, there is also this useful quickstart guide for getting started quickly:[Quickstart Guide](https://flask.palletsprojects.com/en/3.0.x/quickstart/)

### Setting up Flask-SQLAlchemy:
Note that Flask-SQLAlchemy is a wrapper around SQLAlchemy, so it will be useful to check out the documentation and tutorial for using SQLAlchemy linked here:
[SQLAlchemy Documentation](https://docs.sqlalchemy.org/en/20/tutorial/index.html)

Then follow [these steps](https://flask-sqlalchemy.palletsprojects.com/en/3.1.x/quickstart/#installation) to get Flask-SQLAlchemy installed, then initialize and configure extensions. It also shows how to define models and create tables.



## 3. Basic useful features
### Flask
Here is the documentation with the basics needed to start developing using Flask. It assumes knowledge of Python, which I think should be safe to assume.
[Flask Basics](https://flask.palletsprojects.com/en/3.0.x/tutorial/)


### Flask-SQLAlchemy:
Here are the basic useful features for using queries with Flask-SQLAlchemy. It shows the basics of things like inserting, deleting and updating in the database, selecting, and finally querying for views.
[Flask-SQLAlchemy Basics](https://flask-sqlalchemy.palletsprojects.com/en/3.1.x/queries/)


## 4. Conclusion
In the dynamic landscape of web development, the tandem use of Flask and Flask-SQLAlchemy emerges as a compelling solution, seamlessly blending simplicity with robust database capabilities. Setting up a Flask application becomes a swift endeavor, marked by the ease of installation and quick configuration. Flask's minimalistic design empowers developers with the freedom to choose and integrate components, facilitating rapid prototyping and efficient development. With the added integration of Flask-SQLAlchemy, the database layer becomes an integral part of the Flask ecosystem, offering a unified and expressive interface for model definition, database querying, and session management. Ultimately, the Flask and Flask-SQLAlchemy duo empowers developers to create scalable, maintainable, and feature-rich web applications.


## 5. Additional Resources
[Here](https://flask.palletsprojects.com/en/3.0.x/) is the overview for the Flask documentation.


[Here](https://flask-sqlalchemy.palletsprojects.com/en/3.1.x/) is an overview for the Flask-SQLAlchemy documentation.


[Here](https://www.youtube.com/watch?v=uZnp21fu8TQ&t=1s&ab_channel=TechWithTim) is a useful video for learning about Flask-SQLAlchemy:

[Here](https://flask.palletsprojects.com/en/2.3.x/errorhandling/) is a link to some common errors that users run into with Flask.



