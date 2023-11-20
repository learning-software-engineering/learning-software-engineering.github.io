# Learning Bootstrap, a CSS Framework

## Table of contents
### [Introduction](#what-is-bootstrap?-1)
### [References](#references-and-resources-1)

## Preface
Here you will learn the basics of how to incorporate Bootstrap into your website-building workflow. This should not serve as an in-depth guide, but rather one that should help you get your foot in the door to begin understanding and using Bootstrap components. Before you start, it is recommended that you have working knowledge of both HTML and CSS. This could be as little as a simple styled website. Although not required, it will be helpful in understanding why Bootstrap is such a widely-used and useful framework when working with CSS. At the end of this guide, you should be able to apply some simple Bootstrap components or formatting into your website.

## What is Bootstrap?
Bootstrap is a CSS Framework that simplifies and standardizes much of the styling process. It does this by including much of the common styling choices as an optional pre-built class that can be attached to HTML elements, most commonly divs or spans. In a typical workflow, you would need to create the CSS for these class yourself in a .css file and import those styles. Over a large project, you might begin to realize that the styles can get messy and/or redundnant. Using Bootstrap's built-in styles would instead allow you to rely on their basic foundational stylistic building blocks, requiring less custom CSS from you.

## Where to begin
The most extensive guide in getting started with Bootstrap is undoubtedly from the official documentation. Everything here will have its corresponding reference on [their website here](https://getbootstrap.com/docs/5.3/getting-started/introduction/).

For starters, you will need to add Bootstrap to your website's HTML files. Following the guide in the link above: 

1. For responsive design, insert `<meta name="viewport" content="width=device-width, initial-scale=1">` inside your `<head> </head>` element.
2. For Bootstrap's CSS, insert `<link href="https://cdn.jsdelivr.net/npm/bootstrap@5.3.2/dist/css/bootstrap.min.css" rel="stylesheet" integrity="sha384-T3c6CoIi6uLrA9TneNEoa7RxnatzjcDSCmG1MXxSR1GAsXEV/Dwwykc2MPK8M2HN" crossorigin="anonymous">` inside your `<head> </head>` element.
3. For Bootstrap's JavaScript, insert `<script src="https://cdn.jsdelivr.net/npm/bootstrap@5.3.2/dist/js/bootstrap.bundle.min.js" integrity="sha384-C6RzsynM9kWDrMNeT87bh95OGNyZPhcTNXj1NW7RuBCsyN/o0jlpcV8Qyq46cDfL" crossorigin="anonymous"></script>` inside your `<body> </body>` element, at the bottom. This allows the use of certain Bootstrap elements that rely on JavaScript. 

For the sake of this tutorial, insert all the above and it should look something like: 
```
<!doctype html>
<html lang="en">
  <head>
    <meta charset="utf-8">

    <-- Reponsive design -->
    <meta name="viewport" content="width=device-width, initial-scale=1">

    <title>Bootstrap demo</title>

    <-- Bootstrap CSS -->
    <link href="https://cdn.jsdelivr.net/npm/bootstrap@5.3.2/dist/css/bootstrap.min.css" rel="stylesheet" integrity="sha384-T3c6CoIi6uLrA9TneNEoa7RxnatzjcDSCmG1MXxSR1GAsXEV/Dwwykc2MPK8M2HN" crossorigin="anonymous">

  </head>
  <body>
    <h1>Hello, world!</h1>

    <-- Bootstrap JavaScript -->
    <script src="https://cdn.jsdelivr.net/npm/bootstrap@5.3.2/dist/js/bootstrap.bundle.min.js" integrity="sha384-C6RzsynM9kWDrMNeT87bh95OGNyZPhcTNXj1NW7RuBCsyN/o0jlpcV8Qyq46cDfL" crossorigin="anonymous"></script>
  </body>
</html>
```

## Bootstrap Basics 
At the heart of Bootstrap is the inclusion of Bootstrap classes into your HTML elements. At the start, you will find yourself constantly looking at documentation to refer to which available class options are available. These classes are used to add styling into your elements as either a Bootstrap component, or a simple shorthand for common CSS adjustments. Some commonly used classes include the adjustment of margins and padding. Here is an example of how each of them can be used in code, along with their corresponding reference. 

[Margins / Padding](https://getbootstrap.com/docs/5.3/utilities/spacing/)
```
<div class="mt-0 ms-1 me-1 mb-0"></div>
<div class="m-1"></div>
<div class="mx-auto my-5"></div>

<div class="pt-4 ps-2 pe-3 pb-0"></div>
<div class="p-auto"></div>
<div class="px-1 py-5"></div>
```

These class names may look foreign, but essentially they follow the format of `[margin / padding][side]-[scale]`. What they do is change the margins or paddings of the HTML elements without the need for custom CSS styling or classes, since it is common to want to adjust spacing conveniently on the fly. The specific selections can be found in the documentation, but a summary is:

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

### Buttons 
[Bootstrap Buttons Resource](https://getbootstrap.com/docs/5.3/components/buttons/)

### Cards
[Bootstrap Cards Resource](https://getbootstrap.com/docs/5.3/components/card/)

### Grid Layout
[Bootstrap Grid Resource](https://getbootstrap.com/docs/5.3/layout/grid/)

## Closing statements
As seen above, Bootstrap styling can speed up the creation of clean and simple designs in your HTML elements. The usage of Bootstrap extends into React, which has slightly different implementation details which can be found [on their official website here](https://react-bootstrap.netlify.app/docs/getting-started/introduction). Hopefully you have a better understanding of what Bootstrap is, how a component can be used in a website, and how to use Bootstrap layouts to format your elements. 

## References and Resources
[]


