# Using Lodash in JavaScript

## Table of Contents
1. [Introduction](#introduction)
2. [Installation](#installation)
3. [Array Manipulation](#array-manipulation)
4. [Object Manipulation](#object-manipulation)
5. [Function Utilities](#function-utilities)
6. [Additional Resources](#additional-resources)

## Introduction
Lodash is a powerful JavaScript utility library that simplifies the handling of arrays, numbers, objects, strings, etc. It's designed to make JavaScript easier by taking the hassle out of working with arrays, numbers, objects, and strings.Lodash makes JavaScript easier by taking the hassle out of working with arrays, numbers, objects, strings, etc.
Lodash’s modular methods are great for:

- **Iterating arrays, objects, & strings**
- **Manipulating & testing values**
- **Creating composite functions**


## Installation
Lodash can be added to your JavaScript project in a few different ways. Here are the most common methods:

- **Using npm**: Run `npm install lodash` in your project directory.
- **Using a CDN**: Include a script tag in your HTML: `<script src="https://cdn.jsdelivr.net/npm/lodash/lodash.min.js"></script>`
- **In nodejs**:
```javascript
// Load the full build.
var _ = require('lodash');
// Load the core build.
var _ = require('lodash/core');
// Load the FP build for immutable auto-curried iteratee-first data-last methods.
var fp = require('lodash/fp');
 
// Load method categories.
var array = require('lodash/array');
var object = require('lodash/fp/object');
```

## Array Manipulation
Lodash provides a variety of functions to work with arrays efficiently. Here are some common methods:

- `_.chunk(array, [size=1])`: Creates an array of elements split into groups the length of `size`. If array can't be split evenly, the final chunk will be the remaining elements.

- `_.difference(array, [values])`: Creates an array excluding all given values.

### Example Usage Array
```javascript
import _ from 'lodash';

//chunk 
let array = [1, 2, 3, 4, 5, 6];
let chunked = _.chunk(array, 2);
console.log(chunked); // Outputs: [[1, 2], [3, 4], [5, 6]]

//difference 
const array1 = [2, 1, 3];
const array2 = [3, 4];
const result = _.difference(array1, array2);
console.log(result);
// Output: [2, 1]
```
## Object-manipulation
Object manipulation is a common task in JavaScript, and Lodash offers a variety of functions to simplify these operations. Below are some examples of how you can use Lodash to work with objects.

`_.assign` is used to copy the values of all enumerable own properties from one or more source objects to a target object.

`_.cloneDeep` creates a deep clone of the value.

`_.merge` is used to merge own and inherited enumerable string keyed properties of source objects into the destination object.

### Example Usage Object
```javascript
import _ from 'lodash';

//assign 
const object = { 'a': 1 };
const other = { 'b': 2, 'c': 3 };
_.assign(object, other);
console.log(object);
// Output: { 'a': 1, 'b': 2, 'c': 3 }

//cloneDeep 
const objects = [{ 'a': 1 }, { 'b': 2 }];
const deep = _.cloneDeep(objects);
console.log(deep[0] === objects[0]);

//merge 
const object1 = {
  'a': [{ 'b': 2 }, { 'd': 4 }]
};

const object2 = {
  'a': [{ 'c': 3 }, { 'e': 5 }]
};

_.merge(object1, object2);
console.log(object1);
// Output: { 'a': [{ 'b': 2, 'c': 3 }, { 'd': 4, 'e': 5 }] }
```
Those method helps you
## Function Utilities in Lodash

Lodash provides a variety of utilities to enhance and control the behavior of functions. Below are examples of some of these utilities.

`_.once` creates a function that is restricted to invoking the provided function only once.

`_.memoize` creates a function that memoizes the result of the provided function. The result is cached based on the arguments provided to the memoized function. In react, it is similar with UseMemo()

`_.partial` creates a function that invokes the provided function with any additional partial arguments prepended to those provided to the new function.


### Example Usage function
```javascript
import _ from 'lodash';
// debounce
const onlyOnce = _.once(() => {
  console.log('This will be logged only once!');
});

onlyOnce(); // 'This will be logged only once!'
onlyOnce(); // No output, as the function has already been called once.

// memoize
const computeExpensiveValue = (a, b) => {
  console.log('Computing...');
  return a + b;
};

// partial 
const memoizedCompute = _.memoize(computeExpensiveValue);
console.log(memoizedCompute(1, 2)); // 'Computing...' and then 3
console.log(memoizedCompute(1, 2)); // Directly 3, without 'Computing...' as it's cached
```

## Additional Resources

For more in-depth learning and advanced usage of Lodash, the following resources can be highly beneficial:

1. **Lodash Official Documentation**: This is the primary resource for understanding Lodash's API. It provides detailed documentation on every function available in the library. [Lodash Documentation](https://lodash.com/docs/)

2. **GitHub Repository**: The Lodash GitHub repository is a great place to understand the development of the library, contribute to its codebase, and view issues and discussions. [Lodash GitHub](https://github.com/lodash/lodash)

3. **Tutorials and Articles**: Various tutorials and articles are available online that provide practical examples and use cases of Lodash. Websites like Medium, Dev.to, and personal blogs of JavaScript developers often have insightful content. [Lodash Medium](https://medium.com/techshots/introduction-to-lodash-4d1518eac63a#:~:text=Lodash%20is%20a%20JavaScript%20library%20which%20provides%20utility%20functions%20for,enhancing%20productivity%20and%20code%20readability.&text=Lodash%20provides%20a%20plethora%20of,when%20dealing%20with%20javascript%20objects.)
