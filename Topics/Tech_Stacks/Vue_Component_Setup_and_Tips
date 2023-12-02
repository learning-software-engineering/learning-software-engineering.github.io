# Setting up Vue 3 Components, How to Use them, and Other Tips!

## Table of Contents

#### [Introduction](#intro)
#### [What is a Vue Component? ](#what)
#### [Format of Vue Components](#format)
#### [Things to watch out for!](#things)
#### [Conclusion](#conclude)

## Introduction <a name="intro"></a>
This is a guide to the inner workings of Vue Components and their usage. It will tell you how to set them up,
what the file format is, and also give general advice and things to watch out for. This guide assumes the reader has basic knowledge of HTML/CSS, as well as Javascript.

If you have no knowledge of Vue or how to set up a Vue project, it is imperative that you follow [Vue's Quick Start](https://vuejs.org/guide/quick-start.html) instructions for doing so.

## What is a Vue Component? Why should I care? <a name="what"></a>
The Vue.js framework is a Javascript component-based programming model for the development of User Interfaces (UI), and is commonly used for Web Applications. It builds on the syntax of HTML, allowing the user to "declaratively" describe what they want the code to do. This allows for a very reactive app, one that responds efficiently to state changes to update the DOM. What this means is, less work needs to be done by the programmer for the HTML to update.

Components are how it's all done. Every .vue file is a Vue Component! In these files, you can condense the 3 key aspects of a webpage, the HTML, code-behind, and CSS styling. This centralization and user-friendliness has made Vue renowned for its simplicity.

## Format of Vue Components<a name="format"></a>
Here is the general format of a Vue Component.

```c
# Example code of a number that increments when clicked
<script setup>
var count = ref(0)
</script>

<template>
  <button @click="count++">Count is: {{ count }}</button>
</template>

<style scoped>
button {
  font-weight: bold;
}
</style>
```
Thankfully, the order of these 3 key aspects in the file doesn't matter. Let's go each by each.

### HTML Template
Ever seen the HTML of a webpage? That and Vue's HTML template are almost identical. Just remember, the root container must be labelled as ```<template>```, and it can only have one container inside that. Inside *that* sub-container though, anything is possible! On top of things like your standard ```<div>```, you can also use **other** Vue Components that you've imported in the script section!

But that's not all. Every component in Vue has funny little properties. Two of the most useful and important are the visibility property, and the for-loop property. Let's take a look at both in action, eh?

```
<div v-if="this.pizza" class="pizza">
    <div
    v-for="(p, pIndex) in this.pizza"
    :key="pIndex"
    class="topping"
    >
        {{printPizzaCheer()}}
        Toppings: {{this.pizza[pIndex].toppings}}
        Toppings: {{p.toppings}}
        Size: {{this.size}}
        
        </PizzaSauce :sauce="alfredo">
    </div>
</div>

<div v-else class="pizza">
Oops, no pizza!
</div>
```
The ```v-if``` attribute needs a boolean value to determine if this component will display. Here it was reliant on the document variable ```this.pizza```, an array of Objects, not being empty. On the same level as that component, you can include one with a ```v-else``` attribute so that something is displayed alternatively.

The component within the first one is of the for-loop type. Here, it'll cycle through the ```this.pizza``` array and print all the ```toppings``` attributes successively, either using a list index (ex. ```this.pizza[pIndex].toppings```), or just the sub-list item itself (ex. ```p.toppings```). At the end of it, it also displays an imported Component known as PizzaSauce, which just contains a string passed to it that says "Alfredo". More on that in a moment.

The syntax is a bit different from Javascript, so you can choose between ```v-for="item in array"``` or ```v-for="(item, index) in array"```, as long as you use the ```:key``` attribute to distinguish the index. This allows you to use both variables locally inside that for-loop.


### CSS
Let's take a magnifying glass to that style section.
```
<style scoped>
button {
  font-weight: bold;
}
</style>
```

The CSS styling in Vue works as it does anywhere else, but with one key difference. See that ```scoped``` attribute in the ```<style>``` tag? When the tag has that attribute, the CSS can only apply to the component it's present in. Removing it however, allows for usage anywhere else in the program. Just...be careful about CSS conflicts and shadowing.

### Script
This is the meat of Vue, where you essentially define the webpage as an Object-Oriented-Programming Class! It can have it's own methods, attributes, as well as import scripts and other components for use! It's a very dense part of learning Vue, so let's do a general example by adding complementary code to the above HTML example.
```
import PizzaSauce from "./PizzaSauce.vue"

export default {
  components: {
    PizzaSauce,
  },
  
data() {
    return {
      pizza: [],
      restaurant: "Domino's"
    };
  },
  
  props: {
    size: {
      type: String
    }
  },

  mounted() {
    console.log("Pizza party started");
    const firstPizza = {toppings: "Pepperoni, Cheese", bread: "Stuffed Crust"};
    this.pizza.push(firstPizza);
  },

  methods: {
      printPizzaCheer() {
          return "Yay pizza!";
      }
  }
```
In ```export default{}```, we can list a variety of helpful tools. Let's go through them bit by bit.

- **Components:**
Remember PizzaSauce from before? Here, we imported it from a separate file. We could have called it whatever we want, as long as we specify in the import statement and in the components attribute within ```export default{}```. Now we can use it in the HTML as we did before.
- **data():**
Here, you can list all the global data variables to be used in this document. It works like a class instance, so they can be accessed through just the name or ```this.item```. Here, we can define pizza as an empty array by default.
- **props**:
This works like ```data()```, being global variables, except these are passed in by whatever higher-level component calls this one. Let's say a ```Party``` component passed in the string "Large", much like how we did with PizzaSauce here:
```
</PizzaSauce :sauce="alfredo">
```
Now we can use it just the same as a data variable!
- **mounted()**:
This is code that run at the initial rendering of the component. Here, we created a Pizza object with the attributes of ```toppings``` and ```bread```, and then pushed it to the global ```pizza``` array.
- **Methods:**
These are document functions that can be run to aid in calculation. We use ```printPizzaCheer()``` to display a nice celebratory message in the HTML.

Remember, all of these are arrays.
## Things to watch out for! <a name="things"></a>
Vue's reactivity and unique way of handling things can prove to be a double-edged sword if not handled properly. Here are some general tips:
- If you want to display a document variable inside a component, be careful that the attributes of that component don't calculate that variable. If they do, the displaying of the variable will cause itself to be recalculated, then redisplayed, then recalculated, etc. onto an infinite loop, as Vue takes reactivity very seriously. In this case, it is recommended you instead display a component where the variable is calculated inside with info passed to it by the current component.
- If you want the changing of a variable to trigger a re-render of the page, it is highly recommended you mark it as **reactive** first in the script section, like so:
```
const count = ref(0)
```
Inside ```ref()```, one must write the desired value. If ```ref()``` isn't used, Vue may throw a warning and go through some undefined and inconsistent behavior. Better safe than sorry.
## Conclusion <a name="conclude"></a>
In conclusion, Vue is cool!
## References
 - [Intro to Vue](https://vuejs.org/guide/introduction.html)
 - [Component Basics](https://vuejs.org/guide/essentials/component-basics.html)
