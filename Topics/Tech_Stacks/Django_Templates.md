# Introduction to Django Templates

## Prerequisites
- HTML &mdash; basic tags
- CSS &mdash; selectors, colours
- Django &mdash; project/app setup, URL design, function-based views

## Introduction 
Django projects typically process data in some way, such as tailoring information to a user. We may want to be able to serve these tailored webpages, but webpages developed with plain HTML do not support dynamic changes.

Django Template Language (DTL) can be used to dynamically generate HTML pages, and other text-based formats such as XML and CSV. This article will introduce basic DTL syntax through generating a simple HTML webpage. As a running example, suppose we have the following static page for our WcDonald's Restaurant website:

```
<!DOCTYPE html>
<html>
    <head>
        <title>WcDonald's</title>
    </head>
    <body>
      <h3>Menu</h3>
          <ul>
            <li>Chicken Wuggets $10.99</li>
            <li>Big Wac $7.99</li>
            <li>Morld Famous Fries $4.99</li>
          </ul>
    </body>
</html>
```

What if we want to change the menu items? Or change the visibility of items on sale, which also change periodically? We can do so by creating a Django template. But first, we must introduce some setup and basic syntax.

## Creating a Template
First, assuming we have setup our Django project, create a folder called `templates` inside the app folder. This is where Django looks for templates by default. Inside, we create HTML templates by using the `.html` extension. The resulting folder structure may resemble the following: 

```
project/
└── app/
    └── templates/
        └── index.html
    └── ...
```

## Context
Context is a dictionary of dynamic data that is passed to a template upon rendering. Later we will see a concrete example on how to do this in a function-based view.

## Basic Syntax
Django templates for webpages involve both static HTML tags, and DTL specific [syntax](https://docs.djangoproject.com/en/4.2/topics/templates/#syntax) including variables, tags, and filters.

### Variables
**Variable Substitution** is done by wrapping the variable name (passed in from the context) with double curly braces: 
```
<li>{{ menu_item }}</li>
```
So this would render as a list item whose text is the value of `menu_item`. If this variable doesn't exist in the given context, then its value is `None` by default, and it would simply render an empty string. However, this can be [configured](https://docs.djangoproject.com/en/1.11/ref/templates/api/#how-invalid-variables-are-handled).

We can also pass in lists and dictionaries. Using a `.` performs a lookup to access by index/attribute:
```
<li>{{ menu_items.0.name }}</li>
```

Assuming menu_items is a list of dictionaries, this would display the first dictionary's name value.

### Built-in Tags
DTL's built-in tags is a convenient way to allow for conditional statements, loops, loading static files, and [more](https://docs.djangoproject.com/en/4.2/ref/templates/builtins/). Tags are characterized by the `%` symbol inside curly braces.

#### Conditional Statements
The syntax and [boolean operators](https://docs.djangoproject.com/en/4.2/ref/templates/builtins/#boolean-operators) for conditionals inside the tags are similar to Python, except it must end with an `{% endif %}` tag.:
```
{% if menu_item.is_special %}
    <li class="special">{{ menu_item.name}}</li>
{% else %}
    <li class="special">{{ menu_item.name}}</li>
{% endif %}
```

#### Loops
We can loop through lists, dictionaries, and its nested variants with the familiar Python syntax. Like conditionals, it must end with an `{% endfor %}` tag:
```
{% for menu_item in menu_items %}
 {% if menu_item.is_special %}
    <li class="special">{{ menu_item.name }} {{ menu_item.price }}</li>
  {% else %}
    <li class="regular">{{ menu_item.name }} {{ menu_item.price }}</li>
  {% endif %}
{% endfor %}
```

#### Including CSS Files
First, we can create a directory called `static` in the root `project` directory. Inside `static`, it is typical to have subdirectories for file types such as images, `.css`, and `.js` files:
```
project/
└── static/
    └── css/
        └── styles.css
    └── js/
    └── img/
└── app/
    └── ...
└── ...
```
With this setup, we have to configure `settings.py`:
```
# Static files (CSS, JavaScript, Images)
# https://docs.djangoproject.com/en/4.2/howto/static-files/
STATIC_URL = 'static/'
STATICFILES_DIRS = [ BASE_DIR / 'static', ]
```

`STATICFILES_DIRS = [ BASE_DIR / 'static', ]` tells Django to look in the `static` folder in the root directory. However, there are times where you may want to have `static` directories in each app directory, which can be configured accordingly.

In the template, we must load the static files with the `{% load static %}` tag, and include a specific file using the `{% static %}` tag. Using the above file structure, we can include the `.css` file:
```
{% load static %}
<link rel="stylesheet" href="{% static 'css/styles.css' %}">
```
Note that the `{% load static %}` tag must be used before any `{% static %}` tag, so it is generally placed at the top of the template.

### Built-in Filters
Vaguely, filters transform variables in some way, including getting a variable's length, formatting a datetime object, converting a string to a title, and [more](https://docs.djangoproject.com/en/4.2/ref/templates/builtins/#filter).  They are characterized by the pipe `|` operator.

The following puts the length of `list` in a paragraph:
```
<p>{{ list | length }}</p>
```

## Putting it together
Revisiting our initial goal, we want to make WcDonald's webpage more configurable and dynamic. First, we create a template `menu.html` inside the app's `templates` folder. We want to allow changes to menu items, and control whether or not they are a special item.

In our body, we can use a loop to display an abritrary number of menu items, and conditionals to decide whether they are a special or not. Additionally, to change the visibility of special items, we can include our `.css` files in the head:
```
{% load static %}
<!DOCTYPE html>
<html>
    <head>
        <title>WcDonald's</title>
        <link rel="stylesheet" href="{% static 'css/menu.css' %}">
    </head>
    <body>
      <h3>Menu</h3>
          <ul>
            {% for menu_item in menu_items %}
              {% if menu_item.is_special %}
                <li class="special">{{ menu_item.name }} {{ menu_item.price }}</li>
              {% else %}
                <li class="regular">{{ menu_item.name }} {{ menu_item.price }}</li>
              {% endif %}
            {% endfor %}
          </ul>
    </body>
</html>
```
If the item is a special, then we can control its class and style it accordingly using the appropriate selector. 

Next, we need to pass in the **context** through a view. The context will determine the menu items and special items. We can create a simple function-based view to serve our menu webpage. Inside this view, we must define our `context` dictionary and pass it into the `menu.html` template to render, using Django's built-in method:
```
from django.shortcuts import render

def view_menu(request):
    template_name = 'menu.html'

    # Create context to pass into template
    menu_items = [
        {
            'name': 'Chicken Wuggets',
            'price': '$10.99',
            'is_special': False
        },
        {
            'name': 'Big Wac',
            'price': '$7.99',
            'is_special': False
        },
        {
            'name': 'Morld Famous Fries',
            'price': '$4.99',
            'is_special': False
        }
    ]

    context = {
        'menu_items': menu_items
    }

    return render(request, template_name, context)
```
This acheives the same webpage as before, but now we can change menu items at will and change the visiblity and inclusion of special items.

Instead of passing in hard-coded context in the above example, a more powerful and practical example would have the context determined from processing the models.

## Conclusion and Final Words
Django templates are used in industry as are convenient, reusable, and flexible. According to the official Django Developers Survey in 2021, [79%](https://lp.jetbrains.com/django-developer-survey-2021-486/) of Django developers use the Django Template Engine.

It is important to note they are rendered on the server side, which may lead to performance issues and poor user experience. However, combining them with JavaScript (AJAX, React, etc.) is an effective way to mitigate this issue.
