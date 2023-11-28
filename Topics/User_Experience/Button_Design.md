# **Button Design**

## **Introduction**
When creating software, 99.9% of the time, we will need at least one button for each page. Buttons are one of the most common interactions between users and software. However, many software developers underestimate how important buttons are in terms of user experience. A poorly designed button can be confusing, misleading, or even fraustrating enough so that users give up on using the softare. On this page, we will introduce multiple ways that a button can be designed, and their implication behind each design.

## **Button Accessibility (with implementation examples using React Native)**
We will be using the libraries below in React Native for implementations of our button design examples.

```
import { AntDesign } from '@expo/vector-icons'; 
import { Button } from 'react-native-elements';
import Icon from 'react-native-vector-icons/FontAwesome';
```

### **Clickable vs Non-Clickable**
While some buttons are design to be clicked, some are there to deliver the message "this is not an option" to users. Buttons play a significant role in user visibility since software users should be able to tell what is an option for them and what is not in a straight-forward way. 

**Code Demo:**
This is a regular button:
```
<Button
  title="Button"
/>
```

And this is a disabled button:
```
<Button
  title="Disabled button"
  disabled
/>
```
More styling can be done by `disabledStyle` and `disabledTitleStyle`. 

And similarly to disabled button, loading button can also be suitable under certain scenario. e.g. click to expand a paragrah. This is a loading button:
```
<Button
  title="Disabled button"
  loading
/>
```
More styling can be done by `loadingStyle` and `loadingTitleStyle`.


### **Solid vs Transparent**
Some buttons are more significant than the others. When designing buttons, there should be a clear priority hierarchy that users can identify which buttons are the most important ones. (e.g. page navigation, proceed, cancel, etc.) If a button is important, we want to have a solid background with outstanding or contrasting colour. On the other side, 

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
For an option in between of entirely solid and entirely transparent, try `type="outline"`.

### **Consistancy**
It's important to keep button designs consistant. From usability heuristics, "users should not have to guess or assume if different words, situations, or actions mean the same thing." For example, if we are using a back arrow for 'going back to the previous page', we should design the exact same button every time when users wish to get back to the previous page.

This is an implementation of back button using AntDesign library.

```
<AntDesign name="left" onPress={() => navigation.navigate('Previous_Page')}/>
<Logo/>
```

### **Reaction**
What should happen when users click on a button? The button appearence should give some hints about what the button is going to do when user click on them. For example, if the button takes users to their user profile page, it should look like a profile icon to aviod possible confusion. Refering to the back arrow example above, it wouldn't be appropirate if going to the next page is implemented using a back arrow instead of forward arrow. Correspondong button reactions are indicated by the `onPress={...}`, in React Native implementation. For more information about common button appearence library, please see Ant Design for details.