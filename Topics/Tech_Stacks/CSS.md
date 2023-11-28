# CSS (Cascading Style Sheets)

## Table of contents
### [Introduction](#introduction-1)
### [CSS Cascade](#css-cascade-1)
### [CSS Selector Specificity](#css-selector-specificity-1)
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

## CSS Selector Specificity:

CSS specificity is the set of rules and calculations that determine which CSS selectors are executed in the CSS Cascade. Understanding this crucial in improving the fluency of a programmer's ability to write functional CSS, since this concept can save many hours of troubleshooting.

#### Specificity Hierarchy
The selector with the highest specificity is chosen to execute on the CSS Cascade. There are 3 selector categories, from most specific to least specific, shown below:

1. **ID**
2. **Classes and Pseudo-classes**
3. **Elements and Pseudo-elements**

#### How is specificity calculated?
All selectors have 3 values, where each value represents the number of instances it contains of the 3 selector categories. For every pair of selectors, the more specific selector is determined by comparing which value is greater from their respective selectors, from left to right.

For example:

`#im-an-id { ... }  /* IDs=1, Classes=0, Elements=0 */` -> Specificity = 100

`.im-a-class { ... }  /* IDs=0, Classes=1, Elements=0 */` -> Specificity = 010

`p { ... }  /* IDs=0, Classes=0, Elements=1 */` -> Specificity = 001

These selectors are ordered from most specific to least specific.

Suppose we introduce a fourth selector:

`#im-the-best-id.im-another-class.im-yet-another-class { ... }  /* IDs=1, Classes=2, Elements=0 */` -> Specificity = 120

This selector would have the highest specificity of all the previous examples. It has the same number of IDs as the first selector, but has 2 more classes, making it more specific.

N.B. that selector combinators and universal selectors have no impact on the specificity calculation, and inline styles of an element have the highest specificity regardless of the categories above. Also, the `!important` declaration overrides all other declarations.

#### Troubleshooting

If you believe that your CSS is behaving in unexpected ways due to selector specificities, here are some steps you can take (in no particular order) to look into what is causing it.

1. Use Browser Developer Tools

Every browser has developer tools that you can take advantage of when debugging your CSS. They allow you to see which selectors have been executed, and which have not. In Google Chrome, Right-Click -> Inspect Element or F12 to access Chrome Dev Tools. Under the styles tab, you can see which styles have been crossed out, meaning that they have not been executed.

![F12](https://media.geeksforgeeks.org/wp-content/uploads/20191014000644/edit-2.jpg)

You can even hover over individual rules to check/uncheck them to enable/disable them!

[Image Source](https://www.geeksforgeeks.org/chrome-inspect-element-tool-shortcut/)

2. Check for inline styles

Inline styles override any styles defined in stylesheets, since they have the highest specificity. It is discouraged to use inline styles, but they may be used as a last resort to achieve the correct styling.

3. Document your styles

Moreso a preventative measure, preplanning and keeping your styles organized is vital to the development of larger projects.

4. [Specificity Calculator](https://specificity.keegan.st/)

A useful tool for checking CSS code that is not evidently clear, and a great sanity check for experienced CSS programmers.

#### Additional Resources:

[Mozilla's Official Documentation](https://developer.mozilla.org/en-US/docs/Web/CSS/Specificity) is useful for looking up important details regarding CSS in general, and contains all up-to-date documentation about how selector specificity is calculated.

[Codepip's Selector Showdown](https://codepip.com/games/selector-showdown/) is a short but fun minigame that is great at conveying the concept of CSS selector specificity in an interactive way. However, it does require a paid subscription to Codepip. It is recommended that should you give this a try, you should also give their other web development games a try as well. A free alternative is [CSS Diner](https://flukeout.github.io/) which is similar in length, and requires the player to code their solutions.

[Pixel Rocket's "What Is CSS Specificity?"](https://www.youtube.com/watch?v=GLS0gvhQG40) is a brief but concise summary of specificity calculations, featuring many visuals to demonstrate the idea.

## CSS Layout: 

The position property in CSS determines the way an HTML element is positioned on a webpage. For example, it can determine whether the position of an HTML element is static and unchanging or relative to the position of other elements. The possition property has 5 possible values, which are described [here](https://www.w3schools.com/css/css_positioning.asp).
 
Flexbox, or the flexible box layout module, is an alternative to using positioning that makes it easier for a webpage to have a responsive layout, meaning that the elements within the flexbox can more easily respond to varying screen or webpage sizes. The positions of elements in the flexbox are relative to other items. [This game](https://flexboxfroggy.com/) is designed to teach Flexbox in an intuitive and fun way. 
 
CSS grid is also a positioning alternative that provides a grid layout module, in order to display HTML elements within a row and column format. It consists of a parent element and child elements. [This game](https://cssgridgarden.com/) can teach CSS grid basics in a visual, interactive and intuitive way. 

## CSS Frameworks 

Native CSS can be difficult to use, so CSS frameworks have been created so developers can use pre-made styles in order to create good looking website components, navigation bars, buttons, etc. in an easier and faster way without needing to know the semantics of CSS. Two popular CSS frameworks include [Tailwind CSS](https://tailwindcss.com/) and [Bootstrap CSS](https://getbootstrap.com/docs/3.4/css/). 

For an introduction to the Tailwind framework, refer to [Getting Stylish and Responsive with Tailwind CSS](./Tailwind.md).

[React-Bootstrap](https://react-bootstrap.github.io/) is a Bootstrap CSS framework specifically for use on React apps. There is also the guide on our wiki [here](./Bootstrap.md) that can get you started on Bootstrap's basics.

Generally, Bootstrap is easier to use and will produce a good looking website in a shorter amount of time, while Tailwind CSS is more customizable and can create more unique looking elements, but requires more of a time investment and is a bit harder to learn and work with compared to Bootstrap. 
