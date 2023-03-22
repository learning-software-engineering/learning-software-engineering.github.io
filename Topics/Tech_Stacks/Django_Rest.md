# Building RESTful APIs using Django Rest Framework

### Prerequisites

Before learning Django Rest Framework, make sure that you have a working knowledge of the following:

 - [Python](https://www.python.org/): High level general purpose programming language.
 - [Django](https://www.djangoproject.com/): Web framework for Python.

### What Is Django Rest Framework?
Django Rest Framework is a popular library for building RESTful APIs with Django. It provides powerful tools for building APIs, including serialization, authentication, and permissions. You can easily create APIs that support multiple formats like JSON and XML that can be consumed by a variety of client applications. To demonstrate the power of Django Rest Framework, we will create a simple API.

### Set-Up

 We first Install virtualenv by running ```python3 -m pip install virtualenv```. This will ensure that we have the necessary package installed to create and manage virtual environments.

 We now set up the virtual environment and activate it using ```python3 -m virtualenv –p `which python3.11` venv ``` and ```source venv/bin/activate``` respectively in the project directory. Note that ```-p `which python3.11` ``` is placed to avoid common issues with python file directory locations. Also, you can replace `python3.11` with the latest available version of python.

 We now install Django and Django Rest Framework using the command ```pip install django djangorestframework```.

 Once installed, we can start a new Django project by running: ```django-admin startproject <project-name>```. This generates the default Django folder structure including several files.

 we may now create a new Django app by running: ```python manage.py startapp <app-name>```.
 
 The project structure should be similar to the following:
 
 ```
 project-name/
│
├── app-name/
│   ├── __init__.py
│   ├── admin.py
│   ├── apps.py
│   ├── models.py
│   ├── serializers.py
│   ├── tests.py
│   ├── urls.py
│   └── views.py
│
├── project-name/
│   ├── __init__.py
│   ├── settings.py
│   ├── urls.py
│   └── wsgi.py
│
└── manage.py
 ```
 
 In order to add Django Rest Framework to your project, open the settings.py file and add 'rest_framework' to the INSTALLED_APPS list: ```INSTALLED_APPS = [..., 'rest_framework']```
 

 ### How it Works
 
 
 After installing and configuring Django Rest Framework, we may now create a simple API. We first create a new model to represent our API resource. To illustrate the use of Django Rest Framework, we'll create a simple model for a todo item with two fields: its title as a CharField, i.e., a string and its complete as a BooleanField, i.e., a boolean value. We first create a new file called models.py in the API app folder by adding the following code:

``` {python}
from django.db import models

class TodoItem(models.Model):
    title = models.CharField(max_length=200)
    completed = models.BooleanField(default=False)
```

Assuming we want to create an API for your TodoItem model that allows clients to create, read, update, and delete TodoItem instances. We may define a serializer class in serializers.py in the app API folder that converts TodoItem instances to JSON. We add the following code in serializers.py:

``` {python}
from rest_framework import serializers
from .models import TodoItem

class TodoItemSerializer(serializers.ModelSerializer):
    class Meta:
        model = TodoItem
        fields = ('id', 'title', 'completed')
```

The code above converts instances of the Todo model to JSON format so that they can be returned in HTTP responses. This is where the TodoItemSerializer class comes in. It is defined in the serializers.py file and inherits from the ModelSerializer class provided by Django Rest Framework and defines the fields that should be serialized and the model that the serializer should be based on. In our case, we want to serialize the id, title, and completed fields of the TodoItem model, so we include these fields in the Meta class of the serializer.

Next, we'll create a view to handle incoming HTTP requests (GET, POST, PUT, PATCH and DELETE). We create a new file called views.py in the API app folder and add the following code:

``` {python}
from rest_framework.generics import ListCreateAPIView, RetrieveUpdateDestroyAPIView
from .models import TodoItem
from .serializers import TodoItemSerializer

class TodoItemList(ListCreateAPIView):
    serializer_class = TodoItemSerializer
    
    def get_queryset(self):
        return TodoItem.objects.filter(completed=True)

class TodoItemDetail(RetrieveUpdateDestroyAPIView):
    serializer_class = TodoItemSerializer
    queryset = TodoItem.objects.all()


```
The code above uses the TodoItemSerializer we previously created to convert the instances to the correct JSON format. To illustrate further on this and its use cases, we consider the TodoItemList view and note that it queries the database by filtering Todo items that are completed. We do this by overriding the get_queryset method of the ListCreateAPIView class and return only the TodoItem instances where completed is True, i.e., Todo item is completed, using the filter method: ```TodoItem.objects.filter(completed=True)```. This way, when the TodoItemList view is accessed with a GET request, only the completed TodoItem instances will be returned in the response.

Finally, we can add a URL configuration for our API. We create a new file called urls.py in the API app folder and add the following code:

``` {python}
from django.urls import path
from .views import TodoItemList, TodoItemDetail

urlpatterns = [
    path('todos/', TodoItemList.as_view()),
    path('todos/<int:pk>/', TodoItemDetail.as_view()),
]
```

All in all, we have now built a simple API with the ability to list, create, update and delete todo list items. One can test the API by starting the Django development server using ``` python3 manage.py runserver ``` and visiting http://localhost:8000/todos/ in a web browser.

### Extra Resources

Here are some official documentation and helpful tutorials for getting familiar with Django Rest Framework

#### Documentation
- [Django Rest](https://www.django-rest-framework.org/)
- [Django Rest API Guide](https://www.django-rest-framework.org/api-guide/)
- [Django Rest Views](https://www.django-rest-framework.org/api-guide/generic-views/)
- [Django Rest Testing](https://www.django-rest-framework.org/api-guide/testing/)

####  Tutorials
- [Django for Beginners](https://www.youtube.com/watch?v=F5mRW0jo-U4)
- [Learn Django](https://learndjango.com/tutorials/official-django-rest-framework-tutorial-beginners)
- [Real Python](https://realpython.com/django-rest-framework-quick-start)
- [Youtube (Corey Schafer)](https://www.youtube.com/watch?v=Uyei2iDA4Hs&list=PL-osiE80TeTtoQCKZ03TU5fNfx2UY6U4p)
