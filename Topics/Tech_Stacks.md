## Tech Stacks

## Django

### 0. Prerequisites:
 - [Python](https://www.python.org/): High level general purpose programming language. 
 - [HTML](https://www.w3schools.com/html/html_intro.asp): A markup language that is used for the creation of web pages. 
 - [CSS](https://www.w3schools.com/css/css_intro.asp): A language used for styling a web page, it often goes hand in hand with HTML.
 

### 1. Introduction
Django is a web framework for Python that allows for the fast development of secure and maintainable websites. It is a versatile, secure, scalable, maintainable, and portable web framework that provides almost everything developers need to build various types of websites. Django also has extensive and up-to-date documentation, it can be extended and its design allows it to be scaled for more website traffic. Django's built-in security measures help developers avoid security mistakes that may occur during the development of a website. Finally, Django is set up in a way that encourages maintainable and reusable code by using components and the grouping of functionality.

### 2. Set-Up

 Start by setting up a virtual environment and activating it. This is done using the ```python3 -m venv myenv ``` command followed by ```source myenv/bin/activate```. More information about virtual environments can be found [here](https://docs.python.org/3/library/venv.html).

 After setting up the virtual environment you can now install Django using the command ```pip install django```.

 Once Django is installed you can move on to creating the project. This is done first by running ```django-admin startproject <project-name>```. This generates the basic folder structure and a few default files project files.

 Take note of ```manage.py```. This python file will allow you to run a set of commands essential to the creation and modification of a Django project. The first use of it is to create a Django App. An app is a subcomponent of a Django project that provides a specific set of functionalities. The command to create an app is ```python manage.py startapp <app-name>```.

You have now created a basic Django project!

 ### 3. How it Works

 #### Project Files:

 Project structure after setting up the project

```
project-name/
│
├── project-name/
│   ├── __init__.py
│   ├── asgi.py
│   ├── settings.py
│   ├── urls.py
│   └── wsgi.py
│
└── manage.py
```
Graphic inspired by [Real Python](https://realpython.com/django-setup/).

For basic Django projects, you will most likely not be implementing any changes in ```_init__.py```, ```agsi.py```, or ```wgsi.py``` so they will be skipped. ```agsi``` and ```wgsi``` are used for deployment and more information about them can be found [here](https://www.infoworld.com/article/3658336/asgi-explained-the-future-of-python-web-development.html).

```settings.py``` is a configuration file that allows for the configuration of settings including the database settings. Some other common settings include time zones and the installed Django apps. 

```urls.py``` is used to map is used to map different Django views to URLs. So when you type in a browser, ```urls.py``` will decide how incoming requests should be handled. Information on views can be found below in the App section. Below is an example of a ```urls.py``` file. 

```
from django.urls import path
from . import views

urlpatterns = [
    path('', views.home, name='home'),
    path('about/', views.about, name='about'),
    path('contact/', views.contact, name='contact'),
]

```

#### App Files:
Project structure after adding an app
```
project-name/
│
├── app-name/
│   │
│   ├── migrations/
│   │   └── __init__.py
│   │
│   ├── __init__.py
│   ├── admin.py
│   ├── apps.py
│   ├── models.py
│   ├── tests.py
│   └── views.py
│
├── project-name/
│   ├── __init__.py
│   ├── asgi.py
│   ├── settings.py
│   ├── urls.py
│   └── wsgi.py
│
└── manage.py
```
Graphic inspired by [Real Python](https://realpython.com/django-setup/).

For basic Django projects, you will most likely not be implementing any changes in ```_init__.py```, ```admin.py``` or ```apps.py``` as the default setting will most likely be adequete. ```admin.py``` allows the user to [customize the admin form](https://docs.djangoproject.com/en/4.1/intro/tutorial07/) and ```apps.py``` allows the user to [configure the application](https://docs.djangoproject.com/en/4.1/ref/applications/).

```models.py``` allows Django to interact with the database of the web application. It allows Django to understand the data to be stored and manipulated. Below is an example of a model for a book.

```
from django.db import models

class Book(models.Model):
    title = models.CharField(max_length=200)
    author = models.CharField(max_length=100)
    description = models.TextField()
    published_date = models.DateField()

    def __str__(self):
        return self.title

```


```urls.py``` acts in almost the same way as the file for the project except the URLs are specific to the app and not the entire project.

```views.py``` is where you will write the backend for your web application. This will probably be where the most substantial amount of code is written. Below is a view using the ```Book``` model from above. It includes a template ```home.html``` which will be explored below.

```
from django.shortcuts import render
from .models import Book

def home(request):
    books = Book.objects.all()
    context = {
        'books': books
    }
    return render(request, 'home.html', context)
```


A more in-depth guide with specifics on how to build a Django app can be found [here](https://docs.djangoproject.com/en/4.1/intro/tutorial01/).

 ### 4. Basic Templates

 None of the instructions above will result in anything visible on the front end other than the admin page. To change this Django uses templates. Templates are HTML files with Django syntax that is similar to python allowing the user to create loops, if statements, and other blocks of code usually not possible in HTML.

 ```
 <!DOCTYPE html>
<html>
  <head>
    <title>{{ title }}</title>
  </head>
  <body>
    <h1>Welcome to {{ title }}!</h1>
    <p>{{ message }}</p>
  </body>
</html>

 ```

 Above is a simple example template. It uses placeholders that act like variables and allow views to pass in information to the template. This is done using the ```render()``` function in ```views.py```.

 ```
### views.py
from django.shortcuts import render

def my_view(request):
    context = {
        'title': 'My Site',
        'message': 'Welcome to my site!'
    }
    return render(request, 'my_template.html', context)
 ```

 In this view, we create a context that stores the values that will be displayed in the template. The ```render()``` function will render the template with the data specified in ```context```.

### 5. Getting the most out of Django

There are several Django extensions and frameworks that allow the user to truly get the most out of Django.

Once a user has finished building their project locally, they may want to deploy their application. An easy and free way to do it is with Heroku. A tutorial of which can be found [here](https://devcenter.heroku.com/articles/deploying-python).

The [Django REST Framework](https://www.django-rest-framework.org/) is a powerful toolkit for building web APIs. It includes features such as serialization and authentication and also allows the user to implement JavaScript frameworks like React and Angular.

For users looking to scale their applications, they can look at [Celery](https://docs.celeryq.dev/en/stable/) as a way to process a large number of messages.

### 6. More resources

Documentation

- [Official documentation](https://www.djangoproject.com/)
- [Mozilla](https://developer.mozilla.org/en-US/docs/Learn/Server-side/Django/Introduction)
- [W3Schools](https://www.w3schools.com/django/)

Video Tutorials
- [freeCodeCamp.org](https://www.youtube.com/watch?v=F5mRW0jo-U4)
- [Programming with Mosh](https://www.youtube.com/watch?v=rHux0gMZ3Eg)