# Intro to Vue Test Utils (VTU)
Vue Test Utils (commonly abbreviated as VTU) are a set of functions that make it easier to test Vue.js components.  It is commonly used
with a test runner for automated testing in software engineering projects.

## Why should I care?
Automated testing is **essential** for any software engineering team.  With automated testing, teams can ensure they ship the most reliable
and robust software to their clients ([Source](https://www.atlassian.com/continuous-delivery/software-testing/automated-testing)).  It can
also provide confidence to teams whenever they make changes to the codebase in that previous software functionality will not suddenly break. 
In a scenario where a developer could make a hard-to-detect breaking change to the codebase, automated testing can catch it before it becomes
a much bigger (*and likely costly*) problem to the team.

Although it is possible to test Vue components without the VTU, it becomes significantly more complex and error prone.
The VTU makes it *much* easier to test your Vue.js components, especially when paired with a popular test runner like Jest.

## How do I install the VTU?
If you have the Node Package Manager (*npm*) or *yarn* installed, type one of the following commands:
```python
# If you have npm
npm install --save-dev @vue/test-utils

# If you have yarn
yarn add --dev @vue/test-utils
```

If you do not have *npm* installed, you can install the Node version manager (*nvm*) which will automatically install *npm* for you.
You can click [here](https://docs.npmjs.com/downloading-and-installing-node-js-and-npm) and follow the documentation to download *nvm*.

If you do not have *yarn*, you can install it after installing *npm* by typing the following command:
```python
npm install --global yarn
```

## How can I integrate the VTU with Jest?
You will need to install an additional package called *vue-jest* and modify some lines in the Jest configuration file.

1. Make sure that Jest is installed by typing the following command:
```python
npm install --save-dev jest
```

2. Install the *vue-jest* package by typing the following command:
```python
npm install --save-dev vue-jest
```

3. Lastly, add the following lines to the *jest.config.js* file:
```python
{
  "jest": {
    "moduleFileExtensions": [
      "js",
      "json",
      "vue"
    ],
    "transform": {
      ".*\\.(vue)$": "vue-jest"
    }
  }
}
```

## More Information
If you would like to explore more about the VTU, the API can be found [here](https://test-utils.vuejs.org/api/).
