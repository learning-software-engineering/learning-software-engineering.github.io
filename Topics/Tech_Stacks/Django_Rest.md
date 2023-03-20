# Building RESTful APIs using Django Rest Framework

### Prerequisites

Before learning Django Rest Framework, make sure that you have a working knowledge of the following:

 - [Python](https://www.python.org/): High level general purpose programming language.
 - [Django](https://www.djangoproject.com/): Web framework for Python.

### What Is Django Rest Framework?
Django Rest Framework is a popular library for building RESTful APIs with Django. It provides powerful tools for building APIs, including serialization, authentication, and permissions. You can easily create APIs that support multiple formats like JSON and XML that can be consumed by a variety of client applications. To demonstrate the power of Django Rest Framework, we will create a simple API.

### Set-Up

 We first set up the virtual environment and activate it using ```python3 -m venv myenv ``` and ```source myenv/bin/activate``` respectively in the project directory.

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

Next, we'll create a serializer to convert our model instances to JSON. We now create a new file called serializers.py in the app API folder and add the following code:

``` {python}
from rest_framework import serializers
from .models import TodoItem

class TodoItemSerializer(serializers.ModelSerializer):
    class Meta:
        model = TodoItem
        fields = ('id', 'title', 'completed')
```

Next, we'll create a view to handle incoming HTTP requests (GET, POST, PUT, PATCH and DELETE). We create a new file called views.py in the API app folder and add the following code:

``` {python}
from rest_framework.generics import ListCreateAPIView, RetrieveUpdateDestroyAPIView
from .models import TodoItem
from .serializers import TodoItemSerializer

class TodoItemList(ListCreateAPIView):
    queryset = TodoItem.objects.all()
    serializer_class = TodoItemSerializer

class TodoItemDetail(RetrieveUpdateDestroyAPIView):
    queryset = TodoItem.objects.all()
    serializer_class = TodoItemSerializer

```

Finally, we can add a URL configuration for our API. We create a new file called urls.py in the API app folder and add the following code:

``` {python}
from django.urls import path
from .views import TodoItemList, TodoItemDetail

urlpatterns = [
    path('todos/', TodoItemList.as_view()),
    path('todos/<int:pk>/', TodoItemDetail.as_view()),
]
```

All in all, we have now built a simple API with the ability to list, create, update and delete todo list items. One can test the API by starting the Django development server using ``` python manage. py runserver ``` and visiting http://localhost:8000/todos/ in a web browser.

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
