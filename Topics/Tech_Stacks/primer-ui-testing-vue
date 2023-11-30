<h1>A Quick Primer on UI Testing in Vue via vue-testing-library</h1>

<h2>Preamble</h2>
This page will introduce you to the concepts (what and why) behind automatically testing UI, and cover the basics of how to do that for a Vue project, using a simple, high level library. <br/> <br/>

For more detail, remember to #ReadTheDocs @ https://testing-library.com/docs/vue-testing-library/intro, as the documentation is almost always a good (arguably, the best) way of learning something, especially as the scope of this primer is intentionally limited. The Vue docs available online are also a good resource in general to consult when using Vue.

This primer assumes that the reader is using npm in a Vue project, and has some basic knowledge about how both of those work. We also assume that you have a test runner of some sort installed (some minimal guidance about this is provided at the end), and that you know how to use that at a basic level.

We will install a library for UI-testing (and give instructions for that) later.

<h2>What’s UI Testing?</h2>
UI testing isn’t actually that different from regular testing, at its core. UI testing simply refers to writing tests to automatically check that your UI **behaves correctly**, and whether it **displays correctly**, especially if there’s logic powering the UI’s behaviour or how it’s displayed.

<h2>Why Test UI?</h2>
Many applications have fairly sophisticated user interfaces, driven by sophisticated behavioural and display logic. 

If your UI behaviour is allowed to break without you realising it, the user can become frustrated or even unable to use the app correctly, **even if all of the data-side of your app is completely correct**. Testing the correctness of your UI logic, **by ensuring your UI behaves and displays in a way you expect**, thus helps ensure a good user experience, and a good development experience (because being surprised by features breaking without warning is very bad for you, too).

To illustrate the point, two examples of UI behaviour that could be worth testing:
* When a user tries to sign up with bad account info, do they get a warning dialog as we expect them to? (Even if the back-end correctly rejects it, if the UI broke here, the user would be confused). <br/>
* When a user tries to open a navigation drawer, does it actually slide open? (If this broke, the user wouldn’t be able to navigate your site at all!).
Your users depend on your UI behaving correctly – so it’s worth testing that it does. <br/>

Luckily, vue makes this (reasonably) easy, using vue-testing-library.

<h2>How do we test stuff?</h2>
<h3>Run the install command</h3>
Start by installing vue-testing-library. This is different from the lower-level (and perhaps more versatile) vue-test-utils library in that it’s higher level, and a bit simpler to use, so that’s what this primer will use.

Note that this section onwards assumes you know the basics of Vue, and what a Vue Component is.

npm install --save-dev @testing-library/vue@5 if you’re using vue2 <br/>
npm install --save-dev @testing-library/vue if you’re using vue3 <br/>
If you’re using vue1 (2015) this guide is not useful. <br/>

<h3>Basic Test Structure</h3>
Vue breaks UI into smaller, reusable components, just like we break code into small, reusable methods. Hence, this primer uses vue-testing-library to test UI at the level of each Vue Component, but this can involve interacting with child components if you’d like to test more complicated behaviours.

<h3>What tools does vue-testing-library give us?</h3>

Before we start writing tests, we should cover the tools you’ll use from vue-testing-library to write them.
Vue-testing-library lets you render a component using the render method.
Vue-testing-library provides query methods that you can use to find rendered UI elements, and lets you fire events via the fireEvent method to interact with them. 
For more details on the different types of queries and events you can use, consult the official documentation’s cheatsheet at https://testing-library.com/docs/vue-testing-library/cheatsheet.

This primer will include just a few useful queries and events to get you started:
* getByText(“text_to_match”) – return exactly one matching DOM node with matching text content. Throws an error if none, or several, found. <br/>
* getAllByText(“text_to_match”) – return the all matching DOM nodeswith matching text content. Throws an error if none found. <br/>
* fireEvent.click(node) – click a rendered DOM node.

As an aside – vue-testing-library intentionally limits the queries it provides so that your tests find elements similarly to how a user would, that is, using visual/accessible means like text content, because the goal of UI testing **is to make sure your UI works for your user**.

You can query by a special attribute: data-test-id to get around this, but the details of this edge case are outside the scope of a quick primer.


<h3>Actually Writing Tests</h3>
Here’s a general workflow you can use for writing a test for a Vue component: <br/>

* Start by importing the Vue component you’re planning to test, and all commands from the vue-testing-library you hope to use.
* Define a new test, however your test runner expects you to.
* Render that component using the render() method – this lets you simulate rendering a component, and interact with it. 
* Find the component using a component query method 
* Interact with the component as you’d expect (click on it, etc.) using the fireEvent method.
* Make assertions about the UI components – e.g. is the button now red after clicking? – to verify it behaves and displays correctly during this miniature user interaction.

<h3>On Running Tests</h3>
Vue-testing-library tests are set up exactly like any other jest test – just make sure to configure jest’s test matchers so that it’s able to find your new tests. <br/> <br/>

Details on jest setup are outside the scope of this primer (it’s a different technology), but the docs are available at: https://jestjs.io/docs/getting-started for you to read.
<br/> <br/>

You can also run tests from this library with vitest.

<h3>A Guiding Idea, and Two Pitfalls to Avoid</h3>
There’s one key principle to remember: **You’re writing UI tests to make sure your UI works for your user.**

This leads to two principles to keep in mind:
* Don’t test internal implementation details (internal state, or any private helper methods) of your components. These are bound to change at any time. The end goal of UI testing is to ensure that your UI works for the user, so **just ensure it works and looks as it should**. <br/>
* Because the goal of your tests is to make sure your UI works as expected for a user, **write your tests to interact with the UI exactly as a user would**; if the user would have to click on a UI element to trigger a behaviour, you should simulate a click in your tests. 
You don’t want to create a situation where a component works in your tests, that uses JavaScript hacks to interact with the component, but breaks for your user when they actually try to click on it. <br/>



