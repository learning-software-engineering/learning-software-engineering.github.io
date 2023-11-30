# Learning SCSS, a CSS Preprocessor

## Table of contents

### [Introduction](#introduction-1)

### [Getting Started](#getting-started-1)

### [Variables](#variables-1)

### [Maps](#maps-1)

### [Nesting](#nesting-1)

### [Partials](#partials-1)

### [Functions](#functions-1)

### [Placeholder Selectors and Extend/Inheritance](#placeholder-selectors-and-extendinheritance-1)

### [Operators](#operators-1)

### [Compiling files to CSS](#compiling-scss-files-into-css-files)

### [References](#references-and-links)

## Introduction

SCSS is a programming language that extends the capabilities of CSS by introducing new syntax to streamline the process of creating stylesheets. SCSS is a superset of CSS which means that all valid CSS code is also valid SCSS code. Due to this, it is recommended that before you start learning SCSS you should have some working knowledge of CSS. You can get started at [this CSS guide](./CSS.md), but it is suggested to have more practice with CSS. Although not required, it is also recomended to use the BEM methodology when creating class names for HTML elements. You can find more information about BEM on [their website here](https://getbem.com/).

CSS, while essential for styling web pages, has limitations that SCSS addresses. One of these limitations is the lack of modularity in CSS whereas SCSS empowers developers to create modular and reusable components, reducing redundancy. SCSS also simplifies some of the clunky syntax for certain CSS features, one such instance of this is with variables. SCSS also inttroduces nesting to CSS, bringing its syntax closer to other popular languages. These are just a few of the changes SCSS brings to CSS to extend its capabilities that will be discussed in this guide.

When giving examples of SCSS syntax, this guide will also display the compiled CSS code as a comparison. By the end of this guide, you should be able to create simple SCSS stylesheets for your website.

## Getting Started

The most in depth guide for getting started with SCSS is the official documentation. Everything here will have its corresponding reference on [their website here](https://sass-lang.com/).

To start you will need to install the sass package to your project. Some methods include:

1. Using Node.js: `npm install -g sass` (Note: this installs the pure javascript implementation and will run slower than the other options listed)
2. Using Chocolatey: `choco install sass`
3. Using Homebrew: `brew install sass/sass/sass`

## [Variables](https://sass-lang.com/documentation/variables/)

CSS already contains variables, however their implementation in SCSS is much less convoluted as seen below:

#### Plain CSS Variables

```css
:root {
  --color: #333;
}

body {
  color: var(--color);
}
```

#### SCSS Variables Syntax

```scss
$color: #333;

body {
  color: $color;
}
```

#### Compliled CSS

```css
body {
  color: #333;
}
```

## [Maps](https://sass-lang.com/documentation/values/maps/)

Maps are immutable lists of key/value pairs and have many uses, one of which is when you want a variable to save multiple possible values for a certain css property as seen below:

#### SCSS

```scss
$font-weights: (
  "regular": 400,
  "medium": 500,
  "bold": 700,
);

h1 {
  font-weight: map.get($font-weights, bold);
}

p {
  font-weight: map.get($font-weights, medium);
}
```

#### Compliled CSS

```css
h1 {
  font-weight: 700;
}

p {
  font-weight: 500;
}
```

## [Nesting](https://sass-lang.com/documentation/style-rules/#nesting)

Nesting provides a much more intuitive way to visualize which HTML elements your CSS rules will apply to as it has a 1-to-1 relationship with the nesting of HTML elements.

#### SCSS

```scss
.containerA {
  ul {
    margin: 0;
    padding: 0;
    list-style: none;
  }

  li {
    display: grid;
  }
}

.containerB {
  ul {
    margin: 10;
    padding: 10;
    list-style: none;
  }

  li {
    display: inline-block;
  }

  a {
    text-decoration: none;
  }
}
```

#### Compliled CSS

```css
.containerA ul {
  margin: 0;
  padding: 0;
  list-style: none;
}

.containerA li {
  display: grid;
}

.containerB ul {
  margin: 10;
  padding: 10;
  list-style: none;
}

.containerB li {
  display: inline-block;
}

.containerB a {
  text-decoration: none;
}
```

### [Parent Selector](https://sass-lang.com/documentation/style-rules/parent-selector/)

Nesting is also the main reason why it is recomended to use the BEM methodology when creating classes for HTML elements when using SCSS as there is a helpful shortcut for when nesting classes using the parent selector `&`. The parent selector is used in nested selectors to refer to the outer selector like so:

#### SCSS

```scss
.parent {
  display: flex;

  &__child {
    color: "red";
  }

  &:hover {
    text-decoration: underline;
  }
}
```

#### Compliled CSS

```css
.parent {
  display: flex;
}

.parent__child {
  color: "red";
}

.parent:hover {
  text-decoration: underline;
}
```

## [Partials](https://sass-lang.com/documentation/at-rules/use/#partials)

Partials allow you to modularize your stylesheets by creating little snippets of code that you can use within other SCSS files. Partials are always named with a leading underscore to let Sass know that it should not be generated into a CSS file. To include a partial named '\_partial.scss' into another file within the same folder include `@use 'partial';` within the file.

## [Functions](https://sass-lang.com/documentation/at-rules/function/)

Functions are exactly what you would expect them to be and are defined using:

```scss
@function <function name>(<arguments...>) { <function body> }
```

Arguments are seperated by commas and named using SCSS variable syntax. To include a default value/make an argument optional, add a colon after the argument name followd by the default value. This looks like:

```scss
@function <function name>($<argument name>: <default value>) { <function body> }
```

If the last argument is followed by `...`, then all extra arguments to that function are passed into that argument as a list. This allows for an arbitrary number of arguments to be passed into a function. This looks like:

```scss
@function <function name>(<arguments>, $<last argument name>...) { <function body> }
```

To return a value from a function use the `@return` at-rule followed by the value you want to return. This looks like:

```scss
@function <function name>(<arguments>) {
    <function body...>
    @return <value>
}
```

## [Placeholder Selectors and Extend/Inheritance](https://sass-lang.com/documentation/at-rules/extend/)

Placeholder selectors look and act very similar to the CSS class slector. The difference is that they start with a `%` and is not included in the compiled CSS. For example:

#### SCSS

```scss
%placeholder {
  font-weight: bold;
}

body,
%placeholder {
  color: "red";
}
```

#### Compliled CSS

```css
body {
  color: "red";
}
```

The question is then, why would we ever use placeholder selectors if they are never compiled?The answer to that is because they can be extended! Using the `@extend` at-rule allows you to share a set of CSS properties from one selector to another. This looks like:

#### SCSS

```scss
%placeholder {
  font-weight: bold;
}

.classA {
  @extend %placeholder;
}

.classB {
  @extend %placeholder;
  color: "red";
}
```

#### Compliled CSS

```css
.classA,
.classB {
  font-weight: bold;
}

.classB {
  color: "red";
}
```

Using placeholder selectors is so great when extending as unlike class selctors, if the placeholder was never extended, it will not clutter up the output CSS file since it will not be compiled.

## [Operators](https://sass-lang.com/documentation/operators/)

SCSS removes the need to use `calc()` when using simple math operations between values of the same type. This means instead of writing `calc(1000px - 400px)` we could simply write `1000px - 400px`. This by itself may not seem useful but it becomes useful when used in combination with variables. It is important to note however that something like `calc(80% - 100px)` cannot be take out of `calc()` since % and px are not of the same type.

## [Compiling SCSS files into CSS files](https://sass-lang.com/guide/#preprocessing)

Once you have created your SCSS files you will need to compile them into CSS files so that your stylesheets can be applied to your website. Some methods to do so include:

1. Run `sass input.scss output.css` in the command line to manually build css files
2. Run `sass --watch input.scss output.css` in the command line to automatically re-compile input.scss when saved into output.css
3. Run `sass --watch INPUT_FOLDER_PATH:OUTPUT_FOLDER_PATH` in the command line to automatically re-compile .scss files within INPUT_FOLDER_PATH when saved into a .css file within OUTPUT_FOLDER_PATH
4. Using the Live Sass Compiler extension in VSCode

## References and Links

[Our Wiki CSS Guide](./CSS.md),
[BEM Website](https://getbem.com/),
[SCSS Website](https://sass-lang.com/),
[Variables](https://sass-lang.com/documentation/variables/),
[Maps](https://sass-lang.com/documentation/values/maps/),
[Nesting](https://sass-lang.com/documentation/style-rules/#nesting),
[Parent Selectors](https://sass-lang.com/documentation/style-rules/parent-selector/),
[Partials](https://sass-lang.com/documentation/at-rules/use/#partials),
[Functions](https://sass-lang.com/documentation/at-rules/function/),
[Placeholder Selectors and Extend/Inheritance](https://sass-lang.com/documentation/at-rules/extend/),
[Operators](https://sass-lang.com/documentation/operators/),
[Compiling SCSS files into CSS files](https://sass-lang.com/guide/#preprocessing)
