# CSS (Cascading Style Sheets) - FlexBox

## Table of contents
### [Introduction](#introduction-1)
### [Flex-Container VS Flex-Item](#flex-container-vs-flex-item-1)
### [Tips and Tricks](#tips-and-tricks-1)
### [Conclusion](#conclusion-1)

## Introduction

Flexible Box Layout or often known as FlexBox, is a CSS layout model that allows us to organize our website in a simple yet effective way. Before this layout was introduced to CSS, there were four other layout modes, that includes:
-	Inline: To organize texts in our webpage
-	Table: To organize in a 2D-grid based system
-	Block: To organize grouped or sections of our webpage
-	Positioned: To specify exact position for items. 

These four layout modes required lots of code to do some simple tasks like “Centering a div”. This is where FlexBox comes in clutch! This not only made coding easier, but also opened CSS Webpage-organization to a whole new level. 

<img width="541" alt="flexbox" src="https://github.com/Raiyankr/CSS-Flexbox/assets/110127056/ebbf9c61-a5db-4f62-bbb7-010acd17009d">

[Image source](https://acciojob.com/blog/untitled-19/)

## Flex-Container VS Flex-Item

There are two things we need to understand in order to use FlexBox. 
- Flex Container: This container will contain some items from our webpage. This container will also define the organization property of the items combined.
- Flex Item: These can be individual components in our webpage (anywhere from a div, to a nested div).

Before we learn about flex containers, lets talk about flex items. These are any component that is nested or "contained" in our flex container. 

```
<div class="flex-container">
  <div><1/div>
  <div>2</div>
  <div>3</div>
  <div>4</div>
</div>
```
![flex-item-example](https://github.com/Raiyankr/CSS-Flexbox/assets/110127056/31a39299-5dc9-42a2-b503-c1b9f038012d)
[Image source](https://www.w3schools.com/css/css3_flexbox_container.asp)

In the above pictures, we have four items in our flex-container. These items will appear in the same order we add them in. It is sufficient to know this much about flex items for now. Let us now learn how we can create a Flex Container. We can do so by using  "_Display: Flex_" property. This simply makes our container *Flex 💪🏻*. 

```
.flex-container{
  display: flex;
}
```

There are lots of other properties that we can play around with in our container such as:
- flex-direction
- flex-wrap
- justify-content
- align-items

These properties can be used to change how we want to oprganize our items (vertically or horizontally), whether we want to center our whole container, whether we want to center our items, how do we want to space the items, etc. The following image shows how we can play around with the flex propoerties to do various tasks:

![flex-properties](https://github.com/Raiyankr/CSS-Flexbox/assets/110127056/27c9a05e-7c0d-472a-b3f7-8afc27a80373)
[Image source](https://www.bitdegree.org/learn/css-flexbox)

To learn more about these properties, [W3Schoole](https://www.w3schools.com/css/css3_flexbox.asp) and [BitDegree](https://www.bitdegree.org/learn/css-flexbox) are great resources!

## Tips and Tricks 

### flex-direction

One of the most commonly used property is "_flex-direction_". This property allows us to change the default axis from horizontal to vertical. We can see an example of this below:

```
.flex-container{
  display: flex;
  flex-direction: column;
}
```

![flex-direction column](https://github.com/learning-software-engineering/learning-software-engineering.github.io/assets/110127056/a004b2b4-b6ea-4500-8b68-4afc6daf87f8)

This changes our primary axis and secondary axis, which will impact two other properties "_justify-content_" for organizing based on the primary axis and "_align-items_" based on the secondary axis. These two axis are also swapped when we use "_flex-direction: column_". Here is an example:

### justify-content & align-items

```
.flex-container{
  display: flex;
  justify-content: center;
}
```
```
.flex-container{
  display: flex;
  align-items: center;
}
```

![image](https://github.com/learning-software-engineering/learning-software-engineering.github.io/assets/110127056/16bf1053-7dfa-4fa3-8112-1f99446cdda4)

The above image shows the difference between  "_justify-content: center_" and "_align-items: center_" for the default row flex direction (also known as horizontally aligned). We can combine these two property to center something in the middle of the screen. Here is how we can do that:

# Combining Properties

```
.flex-container{
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: center; 
}
```

One last nice property we can use is "_flex-wrap_". This property will make sure as our window size shrinks (based on our primary axis), it will move around the flex items to fit inside the container. It will make sure the items are not onverflowing outside the screen. Here is how we can use it:

```
.flex-container{
  display: flex;
  flex-wrap: wrap;
}
```
![items before wrap](https://github.com/learning-software-engineering/learning-software-engineering.github.io/assets/110127056/a1bda3c7-74ff-47db-8265-dc99e9e20453)

![items after wrap](https://github.com/learning-software-engineering/learning-software-engineering.github.io/assets/110127056/7a8c018a-97cf-49a6-bb46-2035313284fc)


## Conclusion 

These are just the surface level information for using flexbox in CSS. There is so much more we can do with it by combining various properties together. If you are curious to learn more about them, feel free to check our the additional resources. I hope this was both educational and fun for you to learn about but remember, don't forget to 💪🏻😎.

### Additional Resources:
- [WebDevSimplified](https://www.youtube.com/watch?v=fYq5PXgSsbE&ab_channel=WebDevSimplified)
- [W3Schoole](https://www.w3schools.com/css/css3_flexbox.asp) 
- [BitDegree](https://www.bitdegree.org/learn/css-flexbox)
