## CSS Animation: 

## Table of contents
### [Introduction](#introduction-1)
### [Components of CSS Animations](#components-of-css-animations-1)
### [Using An Animation](#using-an-animation-1)
### [Summary](#summary-1)
### [References and Links](#references-and-links-1)

## Introduction

Native CSS has built in animation functionality which can be used to implement web page animations (i.e. on HTML elements) without the use of JavaScript. There are three key advantages to using CSS animation rather than traditional script-driven animation techniques:
1. They easy to use for simple animation; does not require knowledge of JavaScript
2. CSS animations run well even under moderate system load (simple animations can still perform poorly in JavaScript under a similar load)
3. CSS animations are controlled by the browser, allowing the browser to optimize performance and efficiency (ex. the browser may reduce the update frequency of animations running tabs that are not currently visible)

At its essence, CSS animations are transitions, and we can describe them as a 'change from one CSS style to another over the dimension of time'. 

## Components of CSS Animations

There are two main parts to CSS Animation:
1. 'animation' properties: these are CSS element properties that allow you to style the animation of that given element
2. '@keyframes' rules: allow you to define animations 

### 'animation' properties

To configure an animation for an HTML element, we must style that element with the 'animation' property or its sub-properties.
All this does is allow you to configure the timing, duration, and other details about how the 'animation sequence' (i.e. @keyframes) will progress.
This does not configure the appearance of the animation, this is specified using '@keyframes' rules, which we'll touch upon later. 

'animation' sub-properties:
- [animation-composition:](https://developer.mozilla.org/en-US/docs/Web/CSS/animation-composition) 
  - Specifies how the styles of an element should be combined with styles of its descendants during the animation.
- [animation-delay:](https://developer.mozilla.org/en-US/docs/Web/CSS/animation-delay) 
  - Sets the delay before an animation starts, allowing you to control when an animation begins after it is triggered.
- [animation-direction:](https://developer.mozilla.org/en-US/docs/Web/CSS/animation-direction) 
  - Defines whether the animation should play in a forward, backward, or alternate direction.
- [animation-duration:](https://developer.mozilla.org/en-US/docs/Web/CSS/animation-duration)
  - Sets the total duration of an animation, indicating how long it takes to complete one cycle.
- [animation-fill-mode:](https://developer.mozilla.org/en-US/docs/Web/CSS/animation-fill-mode)
  - Determines how the styles are applied to an element before and after the animation, including options like filling backwards or forwards.
- [animation-iteration-count:](https://developer.mozilla.org/en-US/docs/Web/CSS/animation-iteration-count) 
  - Specifies the number of times an animation cycle should be played before stopping.
- [animation-name:](https://developer.mozilla.org/en-US/docs/Web/CSS/animation-name)
  - Assigns a name to the animation, referencing a keyframe rule that defines the styles for each animation state.
- [animation-play-state:](https://developer.mozilla.org/en-US/docs/Web/CSS/animation-play-state) 
  - Controls whether an animation is running or paused, providing dynamic control over the animation's playback.
- [animation-timeline:](https://developer.mozilla.org/en-US/docs/Web/CSS/animation-timeline) 
  - Determines the timeline to which the animation belongs, allowing synchronization with other animations.
- [animation-timing-function:](https://developer.mozilla.org/en-US/docs/Web/CSS/animation-timing-function) 
  - Defines the acceleration curve for an animation, specifying how the intermediate values are calculated over the duration of the animation.

The 'animation' property itself encompasses the above sub-properties and can be used as shorthand to declare all the above properties in one statement (more on this after)

[Link to learn more about 'animation' and its sub-properties:](https://developer.mozilla.org/en-US/docs/Web/CSS/animation)

### Using 'animation' and its sub-properties:

There are two ways to set an the CSS animation style of an HTML element: 
- Using 'animation' property directly (shorthand):
``` CSS 
p {
  animation: 3s infinite alternate slidein;
}
```
this was is useful for saving space

- Using and setting the sub-properties individually:
``` CSS 
p {
  animation-duration: 3s;
  animation-name: slidein;
  animation-iteration-count: infinite;
  animation-direction: alternate;
}
```

### '@keyframes' rules

When we define an '@keyframes' rule we are essentially defining a transition between CSS element style properties. In other words we are defining an animation.

Here's an example:
``` CSS 
@keyframes example {
  from {background-color: red;}
  to {background-color: yellow;}
}
```

There are two types of keywords called "keyframes" (don't get this mistaken with '@keywords' as a rule, which means the animation itself) we can use to determine how the transition will behave and when CSS style changes will occur over time:
1. **Percentage keyframes**:
Setting a percentage keyframe is like setting markers for when a change will occur based on the percentage of the animation that's been completed (ex. CSS styles within a 25% keyframe triggers when the animation is 25% finished). Here's an example:
``` CSS
@keyframes slidein {
  75% {
    font-size: 300%;
    margin-left: 25%;
    width: 150%;
  }
}
```
2. **'from' and 'to' keyframes**:
'from' essentially means at the beginning of the animation (0%). Similiarly, 'to' means at the end of the animation (100%).
Here's an example:
``` CSS
@keyframes slidein {
  from {
    margin-left: 100%;
    width: 300%;
  }

  to {
    margin-left: 0%;
    width: 100%;
  }
}
```
3. **combine both 'from' and 'to' and percentage keyframes**:
``` CSS
@keyframes slidein {
  from {
    margin-left: 100%;
    width: 300%;
  }

  75% {
    font-size: 300%;
    margin-left: 25%;
    width: 150%;
  }

  to {
    margin-left: 0%;
    width: 100%;
  }
}
```

## Using An Animation

If we want to an HTML element to use an animation (i.e. @keyframes rule) we've declared, we must 'bind' that animation to the HTML element. There are two ways to do this depending on if you're using 'animation' property shorthand or sub-properties:
1. 'animation' property:
``` CSS
p {
  animation: 3s infinite alternate <name of animation>;
}
```
2. sub-properties:
``` CSS
p {
  animation-duration: 3s;
  animation-name: <name of animation>;
}
```

## Summary

Summarizing everything we've covered so far:
- Animations are defined using '@keyframes' rules which define the CSS style changes that occur and how the animation will look(ex. background-color: black to background-color: red)
- In '@keyframes' rules we set keyframes using either 'from' or 'to' keyframes, or percentage keyframes (each keyframe represents CSS style values at that particular part of the animation)
- In each specific HTML element, we define how the animation 'binded' to that element will behave
- We configure the 'binded' animations behaviour through using 'animation' property or its various sub-properties (ex. animation-duration: 3s;)

## References and Links
- https://www.youtube.com/watch?v=HZHHBwzmJLk
- https://www.w3schools.com/css/css3_animations.asp
- https://developer.mozilla.org/en-US/docs/Web/CSS/CSS_animations/Using_CSS_animations
- https://developer.mozilla.org/en-US/docs/Web/CSS/animation
