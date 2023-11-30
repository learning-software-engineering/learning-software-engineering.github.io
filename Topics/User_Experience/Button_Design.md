# **Button Design**

## **Introduction**
When creating software, 99.9% of the time, we will need at least one button for each page. Buttons are one of the most common interactions between users and software. However, many software developers underestimate how important buttons are in terms of user experience. 

A poorly designed button can be confusing, misleading, or even frustrating enough that users give up on using the software. Here is an example:

<img width="259" alt="poor_design" src="https://github.com/learning-software-engineering/learning-software-engineering.github.io/assets/90407968/e6aeacd0-8853-4c1b-8737-ba21ac5b70aa">


This is a wrongly designed login page. Users will be confused about the priorities of those three solid buttons. The most important button 'LOGIN ME' is the one that deserves the most user attention. How can we do better?

On this page, we will introduce multiple ways that a button can be designed, and their implication behind each design.

## **Button Accessibility (with implementation examples using React Native)**
We will be using the libraries below in React Native for implementations of our button design examples.

 AntDesign library gives us access to many frequently used elements. Button library enables the touchable elements used to interact with the screen. While Icons library serves as the visual indicators used to describe action or intent. 

```
import { AntDesign } from '@expo/vector-icons'; 
import { Button } from 'react-native-elements';
import Icon from 'react-native-vector-icons/FontAwesome';
```

### **Clickable vs Non-Clickable**
While some buttons are designed to be clicked, some are there to deliver the message "this is not an option" to users. This kind of button is often needed in the developing phase. When developers want to present their software functionalities to their stakeholders, we want their potential users to see what the software could do, eventually. Buttons play a significant role in user visibility since software users should be able to tell what is an option for them and what is not in a straightforward way. 

**Code Demo:**

This is a regular button:
```
<Button
  title="Button"
/>
```
<img width="245" alt="solid" src="https://github.com/learning-software-engineering/learning-software-engineering.github.io/assets/90407968/27f9666f-6801-441a-b4d8-df1a2f4f4e65">

This is a disabled button:

<img width="245" alt="disabled" src="https://github.com/learning-software-engineering/learning-software-engineering.github.io/assets/90407968/5f1fa164-064d-4dce-91f6-20f0248f9a92">

```
<Button
  title="Disabled button"
  disabled
/>
```
More styling can be done by `disabledStyle` which modifies the button wrapping style and `disabledTitleStyle` which controls the style of the text on top of the button. 

And similarly to the disabled button, loading button can also be suitable under certain scenarios. e.g. click to expand a paragraph. This is a loading button:

<img width="245" alt="loading" src="https://github.com/learning-software-engineering/learning-software-engineering.github.io/assets/90407968/ad460842-3b30-4394-bb61-799f81d3a529">

```
<Button
  title="Disabled button"
  loading
/>
```
More styling can be done by `loadingStyle` and `loadingTitleStyle`.


### **Solid vs Transparent**
Some buttons are more significant than others. When designing buttons, there should be a clear priority hierarchy so that users can identify which buttons are the most important ones. (e.g. page navigation, proceed, cancel, etc.) If a button is important, we want to have a solid background with outstanding or contrasting colours. 

<img width="491" alt="solid vs transparent" src="https://github.com/learning-software-engineering/learning-software-engineering.github.io/assets/90407968/ffdf9f14-677c-4960-96cc-3f8224d23cb3">

**Code Demo:**
This is a solid blue button:
```
<Button
  title="Solid Button",
  color="blue"
/>
```
This is a transparent button:

```
<Button
  title="Clear Button"
  type="clear"
/>
```
For an option in between entirely solid and entirely transparent, try `type="outline"`.

### **Consistancy**
It's important to keep button designs consistent. From usability heuristics, "users should not have to guess or assume if different words, situations, or actions mean the same thing." For example, if we are using a back arrow for 'going back to the previous page', we should design the exact same button every time when users wish to get back to the previous page.

This is an implementation of the back button using AntDesign library.

```
<AntDesign name="left" onPress={() => navigation.navigate('Previous_Page')}/>
<Logo/>
```

### **Reaction**
What should happen when users click on a button? The button appearance should give some hints about what the button is going to do when the user clicks on it. For example, if the button takes users to their user profile page, it should look like a profile icon to avoid possible confusion. Referring to the back arrow example above, it wouldn't be appropriate if going to the next page is implemented using a back arrow instead of a forward arrow. Corresponding button reactions are indicated by `onPress={...}`, in React Native implementation. 

For more information about frequently used buttons, please check out the links below and the Ant Design page for details.

References:
https://reactnativeelements.com/
https://docs.expo.dev/ui-programming/react-native-styling-buttons/
