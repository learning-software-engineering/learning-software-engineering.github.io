# Learning Bootstrap, a CSS Framework

## Table of contents
### [Introduction](#what-is-bootstrap?-1)
### [What is Bootstrap](#what-is-bootstrap-1)
### [Where to begin](#where-to-begin-1)
### [Bootstrap Basics](#bootstrap-basics-1)
### [References](#references-and-links-1)

## Preface
Here you will learn the basics of how to incorporate Bootstrap into your website-building workflow. This should not serve as an in-depth guide, but rather one that should help you get your foot in the door to begin understanding and using Bootstrap components. Before you start, it is recommended that you have working knowledge of both HTML and CSS. This could be as little as a simple styled website. You can get started at [this CSS guide](./CSS.md), but it is suggested to have more practice with CSS. Although not required, it will be helpful in understanding why Bootstrap is such a widely-used and useful framework when working with CSS. At the end of this guide, you should be able to apply some simple Bootstrap components or formatting into your website.

## What is Bootstrap?
Bootstrap is a CSS Framework that simplifies and standardizes much of the styling process. It does this by including much of the common styling choices as an optional pre-built class that can be attached to HTML elements, most commonly divs or spans. In a typical workflow, you would need to create the CSS for these class yourself in a .css file and import those styles. Over a large project, you might begin to realize that the styles can get messy and/or redundnant. Using Bootstrap's built-in styles would instead allow you to rely on their basic foundational stylistic building blocks, requiring less custom CSS from you.

## Where to begin
The most extensive guide in getting started with Bootstrap is undoubtedly from the official documentation. Everything here will have its corresponding reference on [their website here](https://getbootstrap.com/docs/5.3/getting-started/introduction/).

For starters, you will need to add Bootstrap to your website's HTML files. Following the guide in the link above: 

1. For responsive design, insert `<meta name="viewport" content="width=device-width, initial-scale=1">` inside your `<head> </head>` element.
2. For Bootstrap's CSS, insert `<link href="https://cdn.jsdelivr.net/npm/bootstrap@5.3.2/dist/css/bootstrap.min.css" rel="stylesheet" integrity="sha384-T3c6CoIi6uLrA9TneNEoa7RxnatzjcDSCmG1MXxSR1GAsXEV/Dwwykc2MPK8M2HN" crossorigin="anonymous">` inside your `<head> </head>` element.
3. For Bootstrap's JavaScript, insert `<script src="https://cdn.jsdelivr.net/npm/bootstrap@5.3.2/dist/js/bootstrap.bundle.min.js" integrity="sha384-C6RzsynM9kWDrMNeT87bh95OGNyZPhcTNXj1NW7RuBCsyN/o0jlpcV8Qyq46cDfL" crossorigin="anonymous"></script>` inside your `<body> </body>` element, at the bottom. This allows the use of certain Bootstrap elements that rely on JavaScript. 

For the sake of this tutorial, insert all the above and it should look something like: 
```html
<!doctype html>
<html lang="en">
  <head>
    <meta charset="utf-8">

    <!--Reponsive design-->
    <meta name="viewport" content="width=device-width, initial-scale=1">

    <title>Bootstrap demo</title>

    <!--Bootstrap CSS-->
    <link href="https://cdn.jsdelivr.net/npm/bootstrap@5.3.2/dist/css/bootstrap.min.css" rel="stylesheet" integrity="sha384-T3c6CoIi6uLrA9TneNEoa7RxnatzjcDSCmG1MXxSR1GAsXEV/Dwwykc2MPK8M2HN" crossorigin="anonymous">

  </head>
  <body>
    <h1>Hello, world!</h1>

    <!--Bootstrap JavaScript-->
    <script src="https://cdn.jsdelivr.net/npm/bootstrap@5.3.2/dist/js/bootstrap.bundle.min.js" integrity="sha384-C6RzsynM9kWDrMNeT87bh95OGNyZPhcTNXj1NW7RuBCsyN/o0jlpcV8Qyq46cDfL" crossorigin="anonymous"></script>
  </body>
</html>
```

## Bootstrap Basics 
At the heart of Bootstrap is the inclusion of Bootstrap classes into your HTML elements. At the start, you will find yourself constantly looking at documentation to refer to which available class options are available. These classes are used to add styling into your elements as either a Bootstrap component, or a simple shorthand for common CSS adjustments. Some commonly used classes include the adjustment of margins and padding. Here is an example of how each of them can be used in code, along with their corresponding reference. 

[Margins / Padding](https://getbootstrap.com/docs/5.3/utilities/spacing/)
```html
<div class="mt-0 ms-1 me-1 mb-0"></div>
<div class="m-1"></div>
<div class="mx-auto my-5"></div>

<div class="pt-4 ps-2 pe-3 pb-0"></div>
<div class="p-auto"></div>
<div class="px-1 py-5"></div>
```

These class names may look foreign, but essentially they follow the format of `[margin / padding][side]-[scale]`. What they do is change the margins or paddings of the HTML elements without the need for custom CSS styling or classes, since it is common to want to adjust spacing conveniently on the fly. Add these classes to any element, and watch the spacing change! The specific selections can be found in the documentation, but a summary is:

```
# Types
m = margin, p = padding

# Sides
t = top, b = bottom, s = start (typically left), e = end (typically right)
x = x-axis (left and right), y = y-axis (top and bottom)
Using m or p alone = all sides

# Values
auto = CSS auto
0, 1, 2, 3, 4, 5 = Relative sizes from 0 to 3 rem
```

### Cards
[Bootstrap Cards Resource](https://getbootstrap.com/docs/5.3/components/card/)

Cards are one of the best places to start to understand how Bootstrap compoments work. They are a simple way to contain a collection of information, and work like their name, as a "card". In essence, they are a rectangular container with a slight border radius to round out the corners that can contain things like an image, a header, a body, and more. Since they do not have margins, you can utilize and append the simple spacing shown in the [previous section](#bootstrap-basics-1).

When starting out with Bootstrap, it is helpful to play around with template code such as the one below. Let's start by breaking down the example code in the reference:


<img width="304" alt="image" src="https://github.com/learning-software-engineering/learning-software-engineering.github.io/assets/88257137/d3dc7fd3-6269-487f-b55d-5998614c6a8b">

```html
<div class="card" style="width: 18rem;">
  <img src="..." class="card-img-top" alt="...">
  <div class="card-body">
    <h5 class="card-title">Card title</h5>
    <p class="card-text">Some quick example text to build on the card title and make up the bulk of the card's content.</p>
    <a href="#" class="btn btn-primary">Go somewhere</a>
  </div>
</div>
```

Here, we have a sample Bootstrap card that will display as the above image. The outer-most element is a div with the `"card"` class, establishing the basic rounded rectangle of width 18rem. This allows for cards to be placed anywhere and adjusted to the appropriate sizes with your own styles. Nested within this element is where you can place other parts of a card, such as `"card-img-top"`, `"card-body"`, `"card-title"`, and `"card-text"`. There are other options you may find on the official documentation, but for now we will focus on these. 

- `"card-img-top"` is a class that can format an image to fill the top of the card. Thus, it is usually attached to an `img` element and can be paired with text in the `"card-body"` that will fill the bottom.
- `"card-body"` is a class where most of the content can be nested inside. The class allots a padded space for your content, such as text, to belong. It can be paired with `"card-title"` and `"card-text"` to format the text within.
- `"card-title"` and `"card-text"` are classes that will style your text. It can be added as a child of the `"card-body"` to utilize the premade formatting, or it can be used on its own with your own custom CSS formatting. 

Reminder that these classes do not have to be placed in this certain order, and liberties can be taken with your own custom CSS to determine the proper formatting that you desire. A lot of Bootstrap components are tools you can use as reference, and you can apply further customization to fit your needs. 

### Grid Layout
[Bootstrap Grid Resource](https://getbootstrap.com/docs/5.3/layout/grid/)

The Bootstrap Grid System is a fundamental tool for creating responsive and organized layouts in web development. It revolves around a 12-column grid structure, providing a flexible framework to arrange content on your webpage.

- **Container:** The `container` class creates a responsive wrapper for your content, adjusting its width based on the screen size.

- **Rows and Columns:** Use the `row` class to define horizontal containers. Inside a row, you can divide the space into 12 columns using classes like `col-`, `col-sm-`, `col-md-`, etc. For example:

  ```html
  <div class="container">
    <div class="row">
      <div class="col-12 col-sm-6">
        <!-- Content for the first column -->
      </div>
      <div class="col-12 col-sm-6">
        <!-- Content for the second column -->
      </div>
    </div>
  </div>
  ```

- **Responsive Classes:** Bootstrap provides responsive classes to control column behavior on different screen sizes. Prefix classes like `col-sm-` for small screens, `col-md-` for medium screens, and so on.

- **Offsetting and Nesting:** Offset classes add space between columns, while nesting allows you to create more intricate layouts by placing rows and columns inside existing columns.

#### Example Implementation

Creating a three-column layout:

```html
<div class="container">
  <div class="row">
    <div class="col-12 col-md-4">
      <!-- Content for the first column -->
    </div>
    <div class="col-12 col-md-4">
      <!-- Content for the second column -->
    </div>
    <div class="col-12 col-md-4">
      <!-- Content for the third column -->
    </div>
  </div>
</div>
```

Mastering the basics of the Bootstrap Grid System empowers you to design responsive and visually appealing web layouts efficiently. Explore different configurations to understand its flexibility and enhance your web development skills. For detailed information, refer to the [Bootstrap Grid documentation](https://getbootstrap.com/docs/5.3/layout/grid/).

## Closing statements
As seen above, Bootstrap styling can speed up the creation of clean and simple designs in your HTML elements. The usage of Bootstrap extends into React, which has slightly different implementation details which can be found [on their official website here](https://react-bootstrap.netlify.app/docs/getting-started/introduction). There are other Frameworks out there, such as Tailwind CSS, which also aim to simplify the styling process, so you can check that out [here](https://tailwindcss.com/docs/installation) Hopefully you have a better understanding of what Bootstrap is, how a component can be used in a website, and how to use Bootstrap layouts to format your elements. 

## References and Links
