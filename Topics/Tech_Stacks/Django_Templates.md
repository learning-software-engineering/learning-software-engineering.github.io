# Introduction to Django Templates

### Prerequisites
- HTML &mdash; basic tags
- CSS &mdash; selectors, colours
- Django &mdash; project/app setup, URL design, function-based views

### Introduction 
Django projects typically process data in some way, such as tailoring information to a user. But webpages developed with plain HTML do not support dynamic changes, so we need a way to generate HTML pages dynamically.

Django Template Language (DTL) is used to dynamically generate HTML, and other text-based formats such as XML, and CSV. This article will introduce basic DTL syntax through generating a simple HTML webpage. As a running example, suppose we have the following static page for our WcDonald's website:

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

What if we want to change the menu items? Or change the colour of items on sale, which also change periodically? Let's start by defining a simple view:

### Creating a Template
First, assuming we have setup our Django project, create a folder called `templates` inside the app folder. This is where Django looks for templates by default. Inside, we create HTML templates by using the `.html` extension. The resulting folder structure may resemble the following: 

```
project
└── app
    └── templates
        └── index.html
    └── ...
```

### Context
Context is dynamic data that is passed to a template upon rendering. In our example, we want to pass in items on the menu, and whether or not an item is on sale. Later we will see a concrete example on how to do this in a function-based view.

### Tags
A Django template for a webpage involves both static HTML tags and DTL specific syntax, including [tags](https://docs.djangoproject.com/en/4.2/ref/templates/builtins/). Tags allow for variable subtitution, conditional statements, and loops.

Variable Substitution is done by wrapping the variable name around double curly braces: 
```
<li>{{ menu_item }}</li>
```


