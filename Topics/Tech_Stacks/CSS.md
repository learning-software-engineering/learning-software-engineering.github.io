# CSS (Cascading Style Sheets)

## Table of contents
### [Introduction](#introduction-1)
### [CSS Cascade](#css-cascade-1)
### [CSS Layout](#css-layout-1)
### [CSS Frameworks](#css-frameworks-1)

## Introduction

CSS, or cascding style sheets, are used to add styles, like spacing and layout, to HTML web pages. While CSS can be done through in-line styles, it is common convention to have a style sheet for the webpage, or the style tag. 

CSS rules consist of a selector and a declaration block, where the selector points to the HTML element or set of elements you want to style and the declaration denotes the style. 

<img width="444" alt="Capture" src="https://user-images.githubusercontent.com/81656509/226232503-8d496905-038e-4f61-b17f-d4f702f75ecf.PNG">

<img width="444" alt="Capture" src="https://user-images.githubusercontent.com/81656509/226232503-8d496905-038e-4f61-b17f-d4f702f75ecf.PNG">

[Image source](https://www.w3schools.com/css/css_syntax.asp)

[W3Schools](https://www.w3schools.com/css/) provides interactive examples and exercises for basic CSS. below provides interactive examples and exercises for basic CSS.

## CSS Cascade

Because of the existence of ids and classes in selectors, often multiple CSS declarations can apply to an HTML element, and they can conflict with each other. The browser needs to resolve these conflicts in order to display the final style onto the website, and this is done through CSS Cascade, which determines which declarations take precedence over others.

[This website](https://wattenberger.com/blog/css-cascade) gives a detailed breakdown of CSS Cascade and its tiers. 


## CSS Layout: 

The position property in CSS determines the way an HTML element is positioned on a webpage. For example, it can determine whether the position of an HTML element is static and unchanging or relative to the position of other elements. The possition property has 5 possible values, which are described [here](https://www.w3schools.com/css/css_positioning.asp).
 
Flexbox, or the flexible box layout module, is an alternative to using positioning that makes it easier for a webpage to have a responsive layout, meaning that the elements within the flexbox can more easily respond to varying screen or webpage sizes. The positions of elements in the flexbox are relative to other items. [This game](https://flexboxfroggy.com/) is designed to teach Flexbox in an intuitive and fun way. 
 
CSS grid is also a positioning alternative that provides a grid layout module, in order to display HTML elements within a row and column format. It consists of a parent element and child elements. [This game](https://cssgridgarden.com/) can teach CSS grid basics in a visual, interactive and intuitive way. 

## CSS Animation: 

Native CSS has built in animation functionality which can be used to implement web page animations without the use of JavaScript. There are three key advantages to using CSS animation rather than traditional script-driven animation techniques:
1. They easy to use for simple animation; does not require knowledge of JavaScript
2. CSS animations run well even under moderate system load (simple animations can still perform poorly in JavaScript under a similar load)
3. CSS animations are controlled by the browser, allowing the browser to optimize performance and efficiency (ex. the browser may reduce the update frequency of animations running tabs that are not currently visible)

At its essence, we can define CSS animations to be 'the change from one CSS style to another over the dimension of time'. 

## CSS Frameworks 

Native CSS can be difficult to use, so CSS frameworks have been created so developers can use pre-made styles in order to create good looking website components, navigation bars, buttons, etc. in an easier and faster way without needing to know the semantics of CSS. Two popular CSS frameworks include [Tailwind CSS](https://tailwindcss.com/) and [Bootstrap CSS](https://getbootstrap.com/docs/3.4/css/). 

[React-Bootstrap](https://react-bootstrap.github.io/) is a Bootstrap CSS framework specifically for use on React apps. There is also the guide on our wiki [here](./Bootstrap.md) that can get you started on Bootstrap's basics.

Generally, Bootstrap is easier to use and will produce a good looking website in a shorter amount of time, while Tailwind CSS is more customizable and can create more unique looking elements, but requires more of a time investment and is a bit harder to learn and work with compared to Bootstrap. 
