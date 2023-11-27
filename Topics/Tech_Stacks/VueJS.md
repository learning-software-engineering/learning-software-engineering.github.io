# Vue.js

## Introduction

Vue.js is an open-source JavaScript framework for building user interfaces and single-page applications. It is known for its ease of integration into projects with other libraries or existing projects, and its capability to power sophisticated Single-Page Applications (SPA) when used in combination with modern tooling and supporting libraries.

---

## Core Features

1. **Reactive Data Binding:** Vue.js offers a reactive and composable data binding system. It provides a straightforward template syntax to declare the state-driven DOM (Document Object Model) rendering.

2. **Components:** Vue's component system allows you to build encapsulated reusable custom elements, which can be composed into complex applications.

3. **Transition Effects:** Vue provides various ways to apply transition effects when items are inserted, updated, or removed from the DOM.

4. **Virtual DOM:** It utilizes a virtual DOM to render UI, ensuring optimal performance by minimizing direct DOM manipulation.

5. **Easy to Learn:** Vue.js is considered one of the easiest frameworks to learn, especially for those who are already familiar with HTML, CSS, and JavaScript.

6. **Ecosystem:** Vue.js has a rich ecosystem supporting routing (Vue Router), state management (Vuex), and build tooling (Vue CLI).

7. **Single File Components (SFC):** A Vue SFC is a file with a `.vue` extension that encapsulates HTML, JavaScript, and CSS in a single file. This approach makes components more modular and easier to maintain. Below is what inside a `.vue` file:
   ```html
   <template>
        <!-- some html here -->
   </template>

   <script>
        // some JS or TS code here
   </script>

   <style>
        /* some css code here*/
   </style>
   ```



## Setting Up

### Prerequisites
- Basic knowledge of HTML, CSS, and JavaScript
- Node.js and npm installed on your system

### Installation(one of the following methods)
- **Using Vue CLI (Recommended):**
    ```
    npm install -g @vue/cli
    vue create my-vue-app
    cd my-vue-app
    npm run serve
    ```

- **Direct `<script>` Include:**
    - You can also include Vue directly in your HTML via a script tag:
        ```html
        <script src="https://cdn.jsdelivr.net/npm/vue@2"></script>
        ```

### Create a Basic Vue instance
- In `.js` or `<script>` in SCF:
    ```js
    import { createApp, ref } from 'vue'

    createApp({
    setup() {
        return {
        count: ref(0)
        }
    }
    }).mount('#app')
    ```

- In `.html` or `<template>` in SCF:
    ```html
    <div id="app">
    <button @click="count++">
        Count is: {{ count }}
    </button>
    </div>
    ```
Here is a simple example of a click counter, where `count` will increment every time the button is clicked.

## Comparison with Other JavaScript Frameworks
### React
- React is more of a library than a full-fledged framework.
- Vue.js is often considered easier to learn due to its simpler syntax.
- React has a larger community and more available resources.

### Angular
- Angular is a full-fledged MVC framework, which is more opinionated than Vue.js.
- Vue.js offers a more lightweight and flexible solution with less overhead.
- Angular's learning curve is steeper compared to Vue.js.


## Useful Links
- [Vue.JS official website](https://vuejs.org)
- Famous projects made with Vue:
  - [GitLab](https://gitlab.com/gitlab-org/gitlab)
  - [Alibaba](https://www.alibaba.com)
  - [Facebook](gttps://www.facebook.com)
  - [Netflix](https://www.netflix.com)