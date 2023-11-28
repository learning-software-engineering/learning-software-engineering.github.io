# Learning React Navigation Library in React Native

## Table of Contents
### [Prerequisites](#prerequisites-1)
### [Introduction](#introduction-1)
### [Installation](#installation-1)
### [Navigation between Screens](#navigation-between-screens-1)
### [Passing Parameters between Screens](#passing-parameters-between-screens-1)
### [Troubleshooting](#troubleshooting-1)
### [Limitations](#limitations-1)

##  Prerequisites
1. [React Native](./ReactNative.md)
2. [React](./React.md)
3. [React Hooks]

## Introduction
React Navigation is a popular and widely used JavaScript library for building navigation and routing in React Native applications. Developed by the React Native community, React Navigation provides a flexible and extensible solution for managing the navigation and user flow within mobile apps.

The library offers a declarative API, allowing developers to define navigation structures in a clear and intuitive manner. React Navigation supports various navigation patterns, such as stack navigation, tab navigation, drawer navigation, and more. It seamlessly integrates with React Native components, enabling the creation of smooth and native-like navigation experiences.

With features like nested navigators, customizable transitions, and deep linking, React Navigation empowers developers to create sophisticated navigation systems that cater to the specific needs of their mobile applications. React Navigation simplifies the process of managing navigation, making it an essential tool for React Native developers.

## Installation
Minimum requirements for installation:
* react-native >= 0.63.0
* expo >= 41 (if you use Expo)
* typescript >= 4.1.0 (if you use TypeScript)

Install using npm:
```npm install @react-navigation/native
npm install react-native-screens react-native-safe-area-context
npm install @react-navigation/native-stack
```

Install using Yarn:
```yarn add @react-navigation/native
yarn add react-native-screens react-native-safe-area-context
yarn add @react-navigation/native-stack
```

Install using pnpm:
```pnpm add @react-navigation/native
pnpm add react-native-screens react-native-safe-area-context
pnpm add @react-navigation/native-stack
```

## Navigation between Screens
### Step 1: Wrapping your app in NavigstionContainer
In your entry file (`index.js` or `App.js`), wrap whole app in `NavigationContainer`.

`NavigationContainer` serve as component responsible for manage all the navigators and navigation state. It's crucial to wrap the entire navigator structure with this component. 

For example:
```
import { NavigationContainer } from '@react-navigation/native';

export default function App() {
  return (
    <NavigationContainer>{/* Your app code */}</NavigationContainer>
  );
}
```

### Step 2: Creating a native stack navigator
`createNativeStackNavigator` is a function containing 2 components: `Screen` and  `Navigator`.  All the pages that need to be navigate should be define as `Screen`, and all the `Screen` should be children of `Navigator` to define the configuration for routes. Each `Screen` object takes a name prop which refers to the name of the route and component prop which specifies the component to render for the route

For example in `App.js`:
```
import { View } from 'react-native';
import { NavigationContainer } from '@react-navigation/native';
import { createNativeStackNavigator } from '@react-navigation/native-stack';

function Page() {
  return (
    <View></View>
  );
}

const Stack = createNativeStackNavigator();

function App() {
  return (
    <NavigationContainer>
      <Stack.Navigator initialRouteName="Page">
        <Stack.Screen name="Page" component={Page} />
      </Stack.Navigator>
    </NavigationContainer>
  );
}

export default App;
```
In the example above, fucntion Page define a screen for our application. We have added this screen into our navigation stack in App() and we set the inital page when we open the app to this page.

### Step 3: Navigation
In step 2 we created a `Screen` component of Page. All the `Screen` component have a prop `navigation` automatically, adn this prop have different functions in which we could use to perform navigation actions. The function we will used for basic navigation is `navigate`. 

The `navigate` method is used to navigate to another screen given the screen name. 

For example we have two page: page1 and page2, code below will navigate page1 to page2:

```
import { Button, View } from 'react-native';
import { NavigationContainer } from '@react-navigation/native';
import { createNativeStackNavigator } from '@react-navigation/native-stack';

function Page1({ navigation }) {
  return (
    <View>
      <Button
        title="Go to Page2"
        onPress={() => navigation.navigate('Page2')}
      />
    </View>
  );
}

function Page2() {
  return (
    <View></View>
  );
}

const Stack = createNativeStackNavigator();

function App() {
  return (
    <NavigationContainer>
      <Stack.Navigator initialRouteName="Page1">
        <Stack.Screen name="Page1" component={Page1} />
        <Stack.Screen name="Page2" component={Page2} />
      </Stack.Navigator>
    </NavigationContainer>
  );
}

export default App;

```

`navigation` prop have another function `goBack`, in which is used to goBack to the previous page. To used it, we could just simply write
```navigation.goBack()```

There are more useful function of `navigation` prop that could be used to perform different tasks. You can read about it more here: https://reactnavigation.org/docs/navigation-prop/

## Passing Parameters between Screens
Sometime, we need to pass different values like ID or current status between screens when we navigate. 

We talked about `navigation.navigate` in the previous section. Actually, `navigation.navigate` can takes in two parameter:
```navigation.navigate(name, params)``` 
The parameter `name` refer the page name we want to navigate to, and the parameter `params` refer to the infomation to pass to the destination route.

From the example above, if we want not only to navigate to page2, but also pass value to page2. We could write:
```
function Page1({ navigation }) {
  return (
    <View>
      <Button
        title="Go to Page2"
        onPress={() => navigation.navigate('Page2', {id: 1})}
      />
    </View>
  );
}
```
We now have passed id of 1 to page2, then we could access this value in page 2 by:
```
function Page2({ route, navigation }) {
  const {id} = route.params
  return (
    <View></View>
  );
}
```
Now we will have a new parameter `route` to Page2. `route` is like `navigation`, which is passed to all the `Screen component`. The value passed in is received and could be accessed in route.params in the destination page.

## Troubleshooting

## Limitations