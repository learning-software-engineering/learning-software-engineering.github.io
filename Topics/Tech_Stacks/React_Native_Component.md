# Common React Native Components

## Summary

This guide provides an overview of commonly-used React Native components for mobile app development.

Key aspects of each component are covered:

- descriptions of the component
- key properties of the component
- links to official documentation for additional information

It aims to serve as a concise study aid and quick reference for developers to understand and effectively use React Native's tools and features.

## Table of contents

- **[Basic UI Components](#basic-ui-components):**
  [View](#View),
  [Text](#Text),
  [Image](#Image),
  [Button](#Button)
- **[List & Scrolling](#list--scrolling):**
  [ScrollView](#ScrollView),
  [FlatList](#FlatList),
  [SectionList](#SectionList)
- **[Interactive Components](#interactive-components):**
  [TextInput](#TextInput),
  [Switch](#Switch),
  [TouchableWithoutFeedback](#TouchableWithoutFeedback),
  [TouchableOpacity](#TouchableOpacity),
  [TouchableHighlight](#TouchableHighlight)
- **[Utilities & Overlay](#utilities--overlay):**
  [StatusBar](#StatusBar),
  [Modal](#Modal),
  [ActivityIndicator](#ActivityIndicator),
  [Linking](#Linking),
  [SafeAreaView](#SafeAreaView),
  [KeyboardAvoidingView](#KeyboardAvoidingView)

### Basic UI components

1. **View** <a id="View"></a>

   1. Explanation:
      A container for arranging and styling other components within the application, similar to div in web development.
   2. Props:
      > - <u>style</u> (object/array): Sets the style of the View.
      > - <u>onLayout</u> (function): Callback when the layout of the View changes.
      > - <u>onStartShouldSetResponder</u> (function): Determines if the View should become the responder when it is tapped or clicked.
      > - <u>onMoveShouldSetResponder</u> (function): Determines if the View should continue to be the responder as it is being moved.
      > - <u>onResponderGrant</u> (function): Callback when the View becomes the responder.
      > - <u>onResponderMove</u> (function): Callback when the responder is being moved.
      > - <u>onResponderRelease</u> (function): Callback when the responder is released.
      > - <u>onResponderTerminate</u> (function): Callback when the responder is terminated.
      > - <u>onResponderTerminationRequest</u> (function): Determines if the View should be terminated as the responder.
   3. Link:  
      View: [https://reactnative.dev/docs/view](https://reactnative.dev/docs/view)  
      Style props in View: [https://reactnative.dev/docs/view-style-props](https://reactnative.dev/docs/view-style-props)

2. **Text** <a id="Text"></a>

   1. Explanation:
      Used to display text.
   2. Props:
      > - <u>style</u> (object/array): Sets the style of the Text.
      > - <u>numberOfLines</u> (number): Sets the limits on the number of lines to display.
      > - <u>ellipsizeMode</u> (string): Defines how to truncate text when it overflows its container. ('head', 'middle', 'tail', 'clip')
      > - <u>onLayout</u> (function): Callback when the layout changes.
      > - <u>adjustsFontSizeToFit</u> (boolean): Determines whether to enable automatic font size adjustment when the content overflows.
      > - <u>minimumFontScale</u> (number): Sets the minimum font scale factor.
      > - <u>allowFontScaling</u> (boolean): Determines whether font scaling should be applied to the Text content.
      > - <u>accessible</u> (boolean): Indicates whether the Text is accessible for users.
      > - <u>accessibilityLabel</u> (string): A label to describe the content of the Text for accessibility.
   3. Link:  
      Text: [https://reactnative.dev/docs/text](https://reactnative.dev/docs/text)  
      Style props in Text: [https://reactnative.dev/docs/text-style-props](https://reactnative.dev/docs/text-style-props)

3. **Image** <a id="Image"></a>

   1. Explanation:
      Used to display different types of images, including network images, static resources, temporary local images, and images from the camera roll.
   2. Props:

      > - <u>style</u> (object/array): Sets the style of the Image.
      > - <u>source</u> (string/require('path')): Sets the source of the image, including URL or a local path.
      > - <u>resizeMode</u> (string): Defines how the image should be resized within its container. ('cover', 'contain', 'stretch', 'repeat', 'center')
      > - <u>onLoad</u> (function): Callback when the image has finished loading.
      > - <u>onLoadStart</u> (function): Callback when the image loading process starts.
      > - <u>onLoadEnd</u> (function): Callback when the image loading process ends, regardless of success or failure.
      > - <u>onError</u> (function): Callback when the image loading process fails.

   3. Link  
      Image: [https://reactnative.dev/docs/image](https://reactnative.dev/docs/image)  
      Styles prop in Image: [https://reactnative.dev/docs/image-style-props](https://reactnative.dev/docs/image-style-props)

4. **Button** <a id="Button"></a>
   1. Explanation:
      A button that allows users to trigger actions with a single tap.
   2. Props:
      > - <u>title</u> (string): Sets the text label that appears on the button.
      > - <u>onPress</u>(function): Calls the function when the button is pressed or tapped.
   3. Link: [https://reactnative.dev/docs/button](https://reactnative.dev/docs/button)

### List & Scrolling

1.  **ScrollView** <a id="ScrollView"></a>

    1. Explanation:
       Provides a scrolling container that can host multiple components and views. Useful for displaying content that exceeds the screen size.
    2. Props:
       > - <u>horizontal</u> (boolean): Determines whether the ScrollView should scroll horizontally.
       > - <u>style</u> (object/array): Sets the style of the ScrollView.
       > - <u>onScroll</u> (function): Callback when the ScrollView is scrolled.
       > - <u>scrollEnabled</u> (boolean): Determines whether scrolling is enabled.
       > - <u>pagingEnabled</u> (boolean): Determines whether to enable paging, making the ScrollView scroll one page at a time.
       > - <u>keyboardDismissMode</u> (string): Defines how the keyboard is dismissed when scrolling. ('none', 'on-drag', 'interactive')
       > - <u>snapToAlignment</u> (string): Defines the alignment for snapped-to items when paging, ('start', 'center', 'end')
       > - <u>snapToInterval</u> (number): Sets the interval between snap points when paging
    3. Link: [https://reactnative.dev/docs/scrollview](https://reactnative.dev/docs/scrollview)

2.  **FlatList** <a id="FlatList"></a>

    1. Explanation:
       A component for rendering efficient scrolling lists. It's better for long lists of data where the number of items might change over time.
    2. Props:
       > - <u>data</u> (array): An array of data items to be rendered in the FlatList.
       > - <u>renderItem</u> (function): A function that returns the component to render for each item in the data. It receives an item from the data and an object with properties like index, item, and separators.
       > - <u>style</u> (object/array): Sets the style of the FlatList.
       > - <u>key</u> (string): An optional key to differentiate multiple FlatList instances when rendering.
       > - <u>keyExtractor</u> (function): A function that extracts a unique key for each item in the data.
       > - <u>horizontal</u> (boolean): Determines whether the FlatList should scroll horizontally (true) or vertically (false).
       > - <u>initialNumToRender</u> (number): Determines the initial number of items to render.
       > - <u>windowSize</u> (number): Sets the number of items in the render window.
       > - <u>onEndReached</u> (function): Callback when the end of the list is reached.
       > - <u>onEndReachedThreshold</u> (number): Sets the threshold distance from the end of the list when onEndReached callback is triggered.
       > - <u>refreshing</u> (boolean): Indicates whether the FlatList is currently refreshing. Use this with the onRefresh prop to implement pull-to-refresh functionality.
       > - <u>onRefresh</u> (function): Callback when the refresh action is triggered.
       > - <u>ListHeaderComponent, ListFooterComponent, ListEmptyComponent</u> (react element): A custom component to render at the top, bottom of the list, or when the data is empty.
    3. Link: [https://reactnative.dev/docs/flatlist](https://reactnative.dev/docs/flatlist)

3.  **SectionList** <a id="SectionList"></a>
    1. Explanation:
       Similar to FlatList, but used for rendering sectioned lists.
    2. Props:
       > - <u>sections</u> (array of objects): An array of section objects, where each section object has a data array and optional key, renderItem, ItemSeparatorComponent, and ListHeaderComponent props.
       > - <u>renderItem</u> (function): A function that returns the component to render for each item within a section. It receives an item from the section's data array and an object with properties like index, item, and section.
       > - <u>style</u> (object/array): Sets the style of the SectionList.
       > - <u>key</u> (string): An optional key to differentiate multiple SectionList instances when rendering.
       > - <u>keyExtractor</u> (function): A function that extracts a unique key for each item in the data.
       > - <u>onEndReached</u> (function): Callback when the end of the list is reached.
       > - <u>onEndReachedThreshold</u> (number): Sets the threshold distance from the end of the list when onEndReached callback is triggered.
       > - <u>refreshing</u> (boolean): Indicates whether the FlatList is currently refreshing. Use this with the onRefresh prop to implement pull-to-refresh functionality.
       > - <u>onRefresh</u> (function): Callback when the refresh action is triggered.
       > - <u>ListHeaderComponent, ListFooterComponent, ItemSeparatorComponentListEmptyComponent</u> (react element): A custom component to render at the top, bottom of the list, between each item, or when the data is empty.
    3. Link: [https://reactnative.dev/docs/sectionlist](https://reactnative.dev/docs/sectionlist)

### Interactive Components

1. **TextInput** <a id="TextInput"></a>

   1. Explanation:
      Allows the user to enter text. It is the basic component for inputting text into the app via a keyboard.
   2. Props:
      > - <u>value</u> (string): The value of the input. Use this to control the input's value in a controlled manner.
      > - <u>onChangeText</u> (function): Callback when the text input value changes.
      > - <u>placeholder</u> (string): The placeholder text that appears when the input is empty.
      > - <u>placeholderTextColor</u> (string): The color of the placeholder text.
      > - <u>keyboardType</u> (string): Specifies the type of keyboard to display. ('default', 'numeric', 'email-address', 'phone-pad', etc.)
      > - <u>autoCapitalize</u> (string): Controls how the text input auto-capitalizes the text. ('none', 'sentences', 'words', and 'characters')
      > - <u>autoCorrect</u> (boolean): Determines whether auto-correction should be enabled for the input.
      > - <u>autoFocus</u> (boolean): Determines whether the input should be focused automatically when the component mounts.
      > - <u>onFocus</u> (function): Callback when the input gains focus.
      > - <u>blurOnSubmit</u> (boolean): Determines if the input should lose focus and blur when the "submit" button is pressed on the keyboard.
      > - <u>onBlur</u> (function): Callback when the input loses focus.
      > - <u>editable</u> (boolean): Determines whether the text input is editable or read-only.
      > - <u>maxLength</u> (number): Sets the maximum number of characters in the input.
      > - <u>multiline</u> (boolean): Indicates whether the input should support multiple lines of text.
      > - <u>secureTextEntry</u> (boolean): Determines whether the text entered is obscured for sensitive information like passwords.
      > - <u>onSubmitEditing</u> (function):Callback when the "submit" button on the keyboard is pressed.
   3. Link: [https://reactnative.dev/docs/textinput](https://reactnative.dev/docs/textinput)

2. **Switch** <a id="Switch"></a>

   1. Explanation:
      Renders a boolean input.
   2. Props:
      > - <u>value</u> (boolean): Determines whether the switch is on.
      > - <u>onValueChange</u> (function): Callback function that is called when the user toggles the switch.
      > - <u>trackColor</u> (object): Sets the color of the track
      > - <u>thumbColor</u> (string): Sets the color of the thumb
      > - <u>disabled</u> (boolean): Determines whether the switch is disabled.
   3. Link:
      [https://reactnative.dev/docs/switch](https://reactnative.dev/docs/switch)

3. **TouchableWithoutFeedback** <a id="TouchableWithoutFeedback"></a>

   1. Explanation:
      A wrapper for providing touchable behavior without any visual feedback when pressed.
   2. Props:
      > - <u>onPress</u> (function): Callback when the button is pressed or tapped.
      > - <u>onLongPress</u> (function): Callback when the button is long-pressed.
      > - <u>onPressIn</u> (function): A callback function that is triggered when the button is initially pressed.
      > - <u>onPressOut</u> (function): A callback function that is triggered when the button is released after being pressed.
      > - <u>pressRetentionOffset</u> (object): An object with top, left, right, and bottom properties that control the distance outside the button where a touch is still considered a press.
      > - <u>hitSlop</u> (object): An object with top, left, right, and bottom properties that extend the touch area for the button beyond its actual bounds.
      > - <u>style</u> (object/array): Sets the style for the TouchableHighlight.
      > - <u>disabled</u> (boolean): Specifies whether the button is in a disabled state and cannot be pressed.
   3. Link: [https://reactnative.dev/docs/touchablewithoutfeedback](https://reactnative.dev/docs/touchablewithoutfeedback)

4. **TouchableOpacity** <a id="TouchableOpacity"></a>

   1. Explanation:
      A wrapper for providing touchable behavior with opacity feedback when pressed.
   2. Props:
      > inherits TouchableWithoutFeedback Props.
      >
      > - <u>activeOpacity</u> (number): Specifies the opacity of the button when it is pressed. Accepts a value between 0 and 1, with 1 being fully opaque.
      > - <u>style</u> (object/array): Sets the style for the TouchableOpacity.
   3. Link: [https://reactnative.dev/docs/touchableopacity](https://reactnative.dev/docs/touchableopacity)

5. **TouchableHighlight** <a id="TouchableHighlight"></a>
   1. Explanation:
      A wrapper for providing touchable behavior with underlay feedback when pressed.
   2. Props:
      > - inherits TouchableWithoutFeedback Props.
      > - <u>activeOpacity</u> (number): Specifies the opacity of the button when it is pressed. Accepts a value between 0 and 1, with 1 being fully opaque. Require underlayColor to be set.
      > - <u>onShowUnderlay</u> (function): Callback when underlay is shown.
      > - <u>onHideUnderlay</u> (function): Callback when underlay is hidden.
      > - <u>underlayColor</u> (string): Sets the color of the underlay that appears when the button is pressed.
      > - <u>style</u> (object/array): Sets the style for the TouchableHighlight.
   3. Link: [https://reactnative.dev/docs/touchablehighlight](https://reactnative.dev/docs/touchablehighlight)

### Utilities & Overlay

1.  **StatusBar** <a id="StatusBar"></a>

    1. Explanation:
       Used to control the appearance of the status bar on the top of the screen that displays important system information such as the time, battery level, network signal strength, and other system status icons.
    2. Props:
       > - <u>animated</u> (boolean): Determines whether changes to the background color or brightness should be animated.
       > - <u>backgroundColor</u> (string): Sets the color, specific to Android
       > - <u>barStyle</u> (string): Sets the style of text and icons. ('default', 'light-content', 'dark-content')
       > - <u>hidden</u> (boolean): Determines whether the status bar should be hidden or visible.
       > - <u>translucent</u> (boolean): Determines whether the status bar should be translucent, making the app draw under the status bar, specific to Android.
       > - <u>networkActivityIndicatorVisible</u> (boolean): Indicates whether the network activity indicator should be visible, specific to iOS.
       > - <u>showHideTransition</u> (string): Defines the transition style for hidden property changes, specific to iOS. ('fade', 'slide')
    3. Link: [https://reactnative.dev/docs/statusbar](https://reactnative.dev/docs/statusbar)

2.  **Modal** <a id="Modal"></a>

    1. Explanation:
       Used for presenting content above an existing screen, typically for dialog boxes, alerts, or custom overlays.
    2. Props:
       > - <u>visible</u> (string): Determines whether the modal is visible.
       > - <u>onRequestClose</u> (function): Callback when the user requests to close the modal, typically through the back button on Android or a swipe-down gesture on iOS.
       > - <u>onShow</u> (function): Callback when the modal is shown.
       > - <u>transparent</u> (boolean): Whether the modal will fill the entire view or be transparent.
       > - <u>animationType</u> (string): Defines how the modal enters and leaves the screen. ('none', 'fade', 'slide', 'slide-up')
       > - <u>supportedOrientations</u> (array of strings): Specifies the orientations that the modal supports. ('portrait', 'portrait-upside-down', 'landscape', 'landscape-left', 'landscape-right')
       > - <u>hardwareAccelerated</u> (boolean): Determines whether to enable hardware acceleration for the modal, specific to Android.
       > - <u>presentationStyle</u> (string): Determines the presentation style of the modal, specific to iOS. ( 'fullScreen', 'pageSheet', 'formSheet', 'overFullScreen'.)
       > - <u>statusBarTranslucent</u> (boolean): Whether to allow the status bar to be translucent, specific to Android.
    3. Link: [https://reactnative.dev/docs/modal](https://reactnative.dev/docs/modal)

3.  **ActivityIndicator** <a id="ActivityIndicator"></a>

    1. Explanation:
       Used to display a spinning indicator, often used to signify that the app is loading or processing something.development
    2. Props:
       > - <u>animating</u> (boolean): Whether to show the spinner.
       > - <u>size</u> (string/number): Set the size of the indicator. ('small', 'large', or a number)
       > - <u>hidesWhenStopped</u> (boolean): Determines whether the indicator should hide when not animating, specific to iOS
       > - <u>color</u> (string): Sets the color of the spinner.
       > - <u>style</u> (object/array): Sets the style of the activity indicator
    3. Link: [https://reactnative.dev/docs/activityindicator](https://reactnative.dev/docs/activityindicator)

4.  **Linking** <a id="Linking"></a>

    1. Explanation:
       Used to add links.
    2. Props:
       > - <u>url</u> (string): Sets the URL.
       > - <u>fallback</u> (object/string): Sets a fallback action if the URL cannot be handled.
       > - <u>target</u> (string): Sets the target for opening the URL, such as '\_blank' for opening in a new window.
       > - <u>onComplete</u> (function/string): Callback when the URL handling operation is complete.
       > - <u>onError</u> (function): Callback when the URL handling operation is failed.
       > - <u>scheme</u> (string): Sets the scheme of the URL, such as 'http', 'https'.
       > - <u>queryParams</u> (object): Defines the query parameters to append to the URL when opening it.
    3. Link: [https://reactnative.dev/docs/linking](https://reactnative.dev/docs/linking)

5.  **SafeAreaView** <a id="SafeAreaView"></a>

    1. Explanation:
       Automatically adjusts the height and position to account for the notch on iOS devices and status bar on Android.
    2. Props:
       > - <u>forcelnset</u> (object): Configures the screen boundaries adjustment. ('top', 'bottom', 'left', 'right' to 'always', 'never', 'conditional').
       > - <u>edges</u> (array)
       > - <u>style</u> (object/array): Sets the style of the safeAreaView.
    3. Link: [https://reactnative.dev/docs/safeareaview](https://reactnative.dev/docs/safeareaview)

6.  **KeyboardAvoidingView** <a id="KeyboardAvoidingView"></a>

    1. Explanation:
       Used to avoid the app being obscured by the on-screen keyboard in text input
    2. Props:
       > - <u>behavior</u> (string): Defines how the view adjusts when the keyboard appears. ('height', 'position', 'padding')
       > - <u>keyboardVerticalOffset</u> (number): Sets an additional offset when the keyboard is displayed, allowing for fine-tuning of the layout.
       > - <u>contentContainerStyle</u> (style): Sets styles to the inner content container of the KeyboardAvoidingView
       > - <u>enabled</u> (boolean): Controls whether the KeyboardAvoidingView is enabled or disabled
    3. Link: [https://reactnative.dev/docs/keyboardavoidingview](https://reactnative.dev/docs/keyboardavoidingview)
