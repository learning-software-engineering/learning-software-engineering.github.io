<h1>A Primer on UI Testing in Vue via vue-testing-library</h1>

<h2>Preamble</h2>
This page will introduce you to the concepts (what and why) behind automatically testing UI, and cover the basics of how to do that for a Vue project.

As always, remember to #ReadTheDocs https://testing-library.com/docs/vue-testing-library/intro, as the documentation is almost always a good (arguably, the best) way of learning something.
The Vue docs available online are also a good resource in general to consult when using Vue.

**<Should I clarify any assumptions I make about the reader, or can I just assume they have npm and stuff?>**

<h2>What’s UI Testing?</h2>
* UI testing = running tests to make sure that your UI behaves correctly.
* Describe what parts of UI we test (behaviour, display logic).

<h2>Why Test UI?</h2>
* Many applications have fairly sophisticated UI, that, with fairly sophisticated behaviour.
* How the UI behaves is very important for the user experience – if the UI is allowed to break without us realizing it, or it is finicky, the user can become frustrated or unable to use the app, even if the data side of your app is correct.
* Ultimately, the logic you use for handling user input and displaying data is still really important to test.
* Vue makes this very convenient.

<h2>Things to Watch out For</h2>
* Considering whether to include a section on common pitfalls?
* I want to just have a quick primer for people, want a very high utility/reading time (the docs are probably a better resource for getting to know stuff deeply – and will be updated more consistently than this, and people don’t like reading).
* The two major pitfalls I want to discuss are:
  * Don’t test implementation details of your components! Don’t touch internal state, or how its private helper methods work – just what it does.
  * You want to interact with tests like a user would, because we’re trying to ensure the component works as we expect when the user uses it. If the user would have to click on it, you should click on it.

<h2>How do we test stuff?</h2>
<h3>Run the install command</h3>
npm install --save-dev @testing-library/vue@5 if you’re using vue2 <br>
npm install --save-dev @testing-library/vue if you’re using vue3 <br>

If you’re using vue1 (2015) this guide is not useful.

<h3>Basic Test Structure</h3>
* Give the user a very basic guide on how to test components
* Rendering components (to then interact with them)
* Finding components
* Interacting with components
* Unsure: Include why the library is designed to only allow certain queries?? Informative for using it in the intended way, but might be extra. 

<h3>Knowledge Stuff: More Query Methods and events</h3>
Probably just link to the documentation for this one to be honest. I could list them here but the documentation will be the supreme authoritative source – and arguably listing a bunch of methods would be outside the scope of a quick primer.
Unsure: It might be a good idea to give the user 2-3 super handy methods to start with, and link the docs for the rest? That would be helpful and it’s reasonably in scope.

<h3>On Running Tests</h3>
Vue-testing-library tests are set up much like any other jest test – but make sure to configure jest’s test matchers so that it’s able to find your new tests. Details on jest setup are outside the scope of this primer (it’s a different technology). But the docs are available at: https://jestjs.io/docs/getting-started for you to read.

You can also run tests from this library with vitest.

