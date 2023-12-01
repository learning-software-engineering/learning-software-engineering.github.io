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
            <li>Big Wac $8.99</li>
            <li>Morld Famous Fries $5.99</li>
          </ul>
    </body>
</html>
```

What if we want to change the menu items? Or change the visibility of items on sale, which also change periodically? We can do so by creating a Django template.

## Creating a Template
First, assuming we have setup our Django project, create a folder called `templates` inside the app folder. This is where Django looks for templates by default. Inside, we create HTML templates by using the `.html` extension. The resulting folder structure may resemble the following: 

```
project
└── app
    └── templates
        └── index.html
    └── ...
```

## Context
Context is a dictionary of dynamic data that is passed to a template upon rendering. In our example, we want to pass in items on the menu, and whether or not an item is on sale. Later we will see a concrete example on how to do this in a function-based view.

## Basic Syntax
A Django webpage template involves both static HTML tags, and DTL specific [syntax](https://docs.djangoproject.com/en/4.2/topics/templates/#syntax) including variables, tags, and filters.

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
We can loop through lists, dictionaries, and its nested variants with the familiar Python syntax. Again, it must end with an `{% endfor %}` tag.:

```
{% for menu_item in menu_items %}
 {% if menu_item.is_special %}
    <li class="special">{{ menu_item.name }} {{ menu_item.price }}</li>
  {% else %}
    <li class="regular">{{ menu_item.name }} {{ menu_item.price }}</li>
  {% endif %}
{% endfor %}
```
#### Loading CSS Files




 

