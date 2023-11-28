# Common React Native Components

## Summary

This guide provides an overview of commonly-used React Native components for mobile app development.

Key aspects of each component are covered:

- descriptions of the component
- key properties of the component
- links to official documentation for additional information

It aims to serve as a concise study aid and quick reference for developers to understand and effectively use React Native's tools and features.

For an example implementation guide of a React Native component, click [here](./React_Native_Component_Example.md).

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
      - style (object/array): Sets the style of the View.
      - onLayuout (function): Callback when the layout of the View changes.
      - onStartShouldSetResponder (function): Determines if the View should become the responder when it is tapped or clicked.
      - onMoveShouldSetResponder (function): Determines if the View should continue to be the responder as it is being moved.
      - onResponderGrant (function): Callback when the View becomes the responder.
      - onResponderMove (function): Callback when the responder is being moved.
      - onResponderRelease (function): Callback when the responder is released.
      - onResponderTerminate (function): Callback when the responder is terminated.
      - onResponderTerminationRequest (function): Determines if the View should be terminated as the responder.
   3. link:
      > View: https://reactnative.dev/docs/view  
      > Style props in View: https://reactnative.dev/docs/view-style-props

2. **Text** <a id="Text"></a>

   1. Explanation:
      Used to display text.
   2. Props:
      - style (object/array): Sets the style of the Text.
      - numberOfLines (number): Sets the limits on the number of lines to display.
      - ellipsizeMode (string): Defines how to truncate text when it overflows its container. ('head', 'middle', 'tail', 'clip')
      - onLayout (function): Callback when the layout changes.
      - adjustsFontSizeToFit (boolean): Determines whether to enable automatic font size adjustment when the content overflows.
      - minimumFontScale (number): Sets the minimum font scale factor.
      - allowFontScaling (boolean): Determines whether font scaling should be applied to the Text content.
      - accessible (boolean): Indicates whether the Text is accessible for users.
      - accessibilityLabel (string): A label to describe the content of the Text for accessibility.
   3. link
      > Text: https://reactnative.dev/docs/text  
      > Style props in Text: https://reactnative.dev/docs/text-style-props

3. **Image** <a id="Image"></a>

   1. Explanation:
      Used to display different types of images, including network images, static resources, temporary local images, and images from the camera roll.
   2. Props:

      - style (object/array): Sets the style of the Image.
      - source (string/require('path')): Sets the source of the image, including URL or a local path.
      - resizeMode (string): Defines how the image should be resized within its container. ('cover', 'contain', 'stretch', 'repeat', 'center')
      - onLoad (function): Callback when the image has finished loading.
      - onLoadStart (function): Callback when the image loading process starts.
      - onLoadEnd (function): Callback when the image loading process ends, regardless of success or failure.
      - onError (function): Callback when the image loading process fails.

   3. link
      > Image: https://reactnative.dev/docs/image  
      > Styles prop in Image: https://reactnative.dev/docs/image-style-props

4. **Button** <a id="Button"></a>
   1. Explanation:
      A button that allows users to trigger actions with a single tap.
   2. Props:
      - title (string): Sets the text label that appears on the button.
      - onPress(function): Calls the function when the button is pressed or tapped.
   3. link
      > https://reactnative.dev/docs/button

### List & Scrolling

1.  **ScrollView** <a id="ScrollView"></a>

    1. Explanation:
       Provides a scrolling container that can host multiple components and views. Useful for displaying content that exceeds the screen size.
    2. Props:
       - horizontal (boolean): Determines whether the ScrollView should scroll horizontally.
       - style (object/array): Sets the style of the ScrollView.
       - onScroll (function): Callback when the ScrollView is scrolled.
       - scrollEnabled (boolean): Determines whether scrolling is enabled.
       - pagingEnabled (boolean): Determines whether to enable paging, making the ScrollView scroll one page at a time.
       - keyboardDismissMode (string): Defines how the keyboard is dismissed when scrolling. ('none', 'on-drag', 'interactive')
       - snapToAlignment (string): Defines the alignment for snapped-to items when paging, ('start', 'center', 'end')
       - snapToInterval (number): Sets the interval between snap points when paging
    3. Link:
       > https://reactnative.dev/docs/scrollview

2.  **FlatList** <a id="FlatList"></a>

    1. Explanation:
       A component for rendering efficient scrolling lists. It's better for long lists of data where the number of items might change over time.
    2. Props:
       - data (array): An array of data items to be rendered in the FlatList.
       - renderItem (function): A function that returns the component to render for each item in the data. It receives an item from the data and an object with properties like index, item, and separators.
       - style (object/array): Sets the style of the FlatList.
       - key (string): An optional key to differentiate multiple FlatList instances when rendering.
       - keyExtractor (function): A function that extracts a unique key for each item in the data.
       - horizontal (boolean): Determines whether the FlatList should scroll horizontally (true) or vertically (false).
       - initialNumToRender (number): Determines the initial number of items to render.
       - windowSize (number): Sets the number of items in the render window.
       - onEndReached (function): Callback when the end of the list is reached.
       - onEndReachedThreshold (number): Sets the threshold distance from the end of the list when onEndReached callback is triggered.
       - refreshing (boolean): Indicates whether the FlatList is currently refreshing. Use this with the onRefresh prop to implement pull-to-refresh functionality.
       - onRefresh (function): Callback when the refresh action is triggered.
       - ListHeaderComponent, ListFooterComponent, ListEmptyComponent (react element): A custom component to render at the top, bottom of the list, or when the data is empty.
    3. link:
       > https://reactnative.dev/docs/flatlist

3.  **SectionList** <a id="SectionList"></a>
    1. Explanation:
       Similar to FlatList, but used for rendering sectioned lists.
    2. Props:
       - sections (array of objects): An array of section objects, where each section object has a data array and optional key, renderItem, ItemSeparatorComponent, and ListHeaderComponent props.
       - renderItem (function): A function that returns the component to render for each item within a section. It receives an item from the section's data array and an object with properties like index, item, and section.
       - style (object/array): Sets the style of the SectionList.
       - key (string): An optional key to differentiate multiple SectionList instances when rendering.
       - keyExtractor (function): A function that extracts a unique key for each item in the data.
       - onEndReached (function): Callback when the end of the list is reached.
       - onEndReachedThreshold (number): Sets the threshold distance from the end of the list when onEndReached callback is triggered.
       - refreshing (boolean): Indicates whether the FlatList is currently refreshing. Use this with the onRefresh prop to implement pull-to-refresh functionality.
       - onRefresh (function): Callback when the refresh action is triggered.
       - ListHeaderComponent, ListFooterComponent, ItemSeparatorComponentListEmptyComponent (react element): A custom component to render at the top, bottom of the list, between each item, or when the data is empty.
    3. link
       > https://reactnative.dev/docs/sectionlist

### Interactive Components

1. **TextInput** <a id="TextInput"></a>

   1. Explanation:
      Allows the user to enter text. It is the basic component for inputting text into the app via a keyboard.
   2. Props:
      - value (string): The value of the input. Use this to control the input's value in a controlled manner.
      - onChangeText (function): Callback when the text input value changes.
      - placeholder (string): The placeholder text that appears when the input is empty.
      - placeholderTextColor (string): The color of the placeholder text.
      - keyboardType (string): Specifies the type of keyboard to display. ('default', 'numeric', 'email-address', 'phone-pad', etc.)
      - autoCapitalize (string): Controls how the text input auto-capitalizes the text. ('none', 'sentences', 'words', and 'characters')
      - autoCorrect (boolean): Determines whether auto-correction should be enabled for the input.
      - autoFocus (boolean): Determines whether the input should be focused automatically when the component mounts.
      - onFocus (function): Callback when the input gains focus.
      - blurOnSubmit (boolean): Determines if the input should lose focus and blur when the "submit" button is pressed on the keyboard.
      - onBlur (function): Callback when the input loses focus.
      - editable (boolean): Determines whether the text input is editable or read-only.
      - maxLength (number): Sets the maximum number of characters in the input.
      - multiline (boolean): Indicates whether the input should support multiple lines of text.
      - secureTextEntry (boolean): Determines whether the text entered is obscured for sensitive information like passwords.
      - onSubmitEditing (function):Callback when the "submit" button on the keyboard is pressed.
   3. link
      > https://reactnative.dev/docs/textinput

2. **Switch** <a id="Switch"></a>

   1. Explanation:
      Renders a boolean input.
   2. Props:
      - value (boolean): Determines whether the switch is on.
      - onValueChange (function): Callback function that is called when the user toggles the switch.
      - trackColor (object): Sets the color of the track
      - thumbColor (string): Sets the color of the thumb
      - disabled (boolean): Determines whether the switch is disabled.
   3. link
      > https://reactnative.dev/docs/switch

3. **TouchableWithoutFeedback** <a id="TouchableWithoutFeedback"></a>

   1. Explanation:
      A wrapper for providing touchable behavior without any visual feedback when pressed.
   2. Props:
      - onPress (function): Callback when the button is pressed or tapped.
      - onLongPress (function): Callback when the button is long-pressed.
      - onPressIn (function): A callback function that is triggered when the button is initially pressed.
      - onPressOut (function): A callback function that is triggered when the button is released after being pressed.
      - pressRetentionOffset (object): An object with top, left, right, and bottom properties that control the distance outside the button where a touch is still considered a press.
      - hitSlop (object): An object with top, left, right, and bottom properties that extend the touch area for the button beyond its actual bounds.
      - style (object/array): Sets the style for the TouchableHighlight.
      - disabled (boolean): Specifies whether the button is in a disabled state and cannot be pressed.
   3. link
      > https://reactnative.dev/docs/touchablewithoutfeedback

4. **TouchableOpacity** <a id="TouchableOpacity"></a>

   1. Explanation:
      A wrapper for providing touchable behavior with opacity feedback when pressed.
   2. Props:
      - inherits TouchableWithoutFeedback Props.
      - activeOpacity (number): Specifies the opacity of the button when it is pressed. Accepts a value between 0 and 1, with 1 being fully opaque.
      - style (object/array): Sets the style for the TouchableOpacity.
   3. link
      > https://reactnative.dev/docs/touchableopacity

5. **TouchableHighlight** <a id="TouchableHighlight"></a>
   1. Explanation:
      A wrapper for providing touchable behavior with underlay feedback when pressed.
   2. Props:
      - inherits TouchableWithoutFeedback Props.
      - activeOpacity (number): Specifies the opacity of the button when it is pressed. Accepts a value between 0 and 1, with 1 being fully opaque. Require underlayColor to be set.
      - onShowUnderlay (function): Callback when underlay is shown.
      - onHideUnderlay (function): Callback when underlay is hidden.
      - underlayColor (string): Sets the color of the underlay that appears when the button is pressed.
      - style (object/array): Sets the style for the TouchableHighlight.
   3. link
      > https://reactnative.dev/docs/touchablehighlight

### Utilities & Overlay

1.  **StatusBar** <a id="StatusBar"></a>

    1. Explanation:
       Used to control the appearance of the status bar on the top of the screen that displays important system information such as the time, battery level, network signal strength, and other system status icons.
    2. Props:
       - animated (boolean): Determines whether changes to the background color or brightness should be animated.
       - backgroundColor (string): Sets the color, specific to Android
       - barStyle (string): Sets the style of text and icons. ('default', 'light-content', 'dark-content')
       - hidden (boolean): Determines whether the status bar should be hidden or visible.
       - translucent (boolean): Determines whether the status bar should be translucent, making the app draw under the status bar, specific to Android.
       - networkActivityIndicatorVisible (boolean): Indicates whether the network activity indicator should be visible, specific to iOS.
       - showHideTransition (string): Defines the transition style for hidden property changes, specific to iOS. ('fade', 'slide')
    3. link
       > https://reactnative.dev/docs/statusbar

2.  **Modal** <a id="Modal"></a>

    1. Explanation:
       Used for presenting content above an existing screen, typically for dialog boxes, alerts, or custom overlays.
    2. Props:
       - visible (string): Determines whether the modal is visible.
       - onRequestClose (function): Callback when the user requests to close the modal, typically through the back button on Android or a swipe-down gesture on iOS.
       - onShow (function): Callback when the modal is shown.
       - transparent (boolean): Whether the modal will fill the entire view or be transparent.
       - animationType (string): Defines how the modal enters and leaves the screen. ('none', 'fade', 'slide', 'slide-up')
       - supportedOrientations(array of strings): Specifies the orientations that the modal supports. ('portrait', 'portrait-upside-down', 'landscape', 'landscape-left', 'landscape-right')
       - hardwareAccelerated (boolean): Determines whether to enable hardware acceleration for the modal, specific to Android.
       - presentationStyle (string): Determines the presentation style of the modal, specific to iOS. ( 'fullScreen', 'pageSheet', 'formSheet', 'overFullScreen'.)
       - statusBarTranslucent (boolean): Whether to allow the status bar to be translucent, specific to Android.
    3. link
       > https://reactnative.dev/docs/modal

3.  **ActivityIndicator** <a id="ActivityIndicator"></a>

    1. Explanation:
       Used to display a spinning indicator, often used to signify that the app is loading or processing something.development
    2. Props:
       - animating (boolean): Whether to show the spinner.
       - size (string/number): Set the size of the indicator. ('small', 'large', or a number)
       - hidesWhenStopped (boolean): Determines whether the indicator should hide when not animating, specific to iOS
       - color (string): Sets the color of the spinner.
       - style (object/array): Sets the style of the activity indicator
    3. link
       > https://reactnative.dev/docs/activityindicator

4.  **Linking** <a id="Linking"></a>

    1. Explanation:
       Used to add links.
    2. Props:
       - url (string): Sets the URL.
       - fallback (object/string): Sets a fallback action if the URL cannot be handled.
       - target (string): Sets the target for opening the URL, such as '\_blank' for opening in a new window.
       - onComplete (function/string): Callback when the URL handling operation is complete.
       - onError (function): Callback when the URL handling operation is failed.
       - scheme (string): Sets the scheme of the URL, such as 'http', 'https'.
       - queryParams (object): Defines the query parameters to append to the URL when opening it.
    3. link
       > https://reactnative.dev/docs/linking

5.  **SafeAreaView** <a id="SafeAreaView"></a>

    1. Explanation:
       Automatically adjusts the height and position to account for the notch on iOS devices and status bar on Android.
    2. Props:
       - forcelnset (object): Configures the screen boundaries adjustment. ('top', 'bottom', 'left', 'right' to 'always', 'never', 'conditional').
       - edges (array)
       - style (object/array): Sets the style of the safeAreaView.
    3. link
       > https://reactnative.dev/docs/safeareaview

6.  **KeyboardAvoidingView** <a id="KeyboardAvoidingView"></a>

    1. Explanation:
       Used to avoid the app being obscured by the on-screen keyboard in text input
    2. Props:
       - behavior (string): Defines how the view adjusts when the keyboard appears. ('height', 'position', 'padding')
       - keyboardVerticalOffset (number): Sets an additional offset when the keyboard is displayed, allowing for fine-tuning of the layout.
       - contentContainerStyle (style): Sets styles to the inner content container of the KeyboardAvoidingView
       - enabled (boolean): Controls whether the KeyboardAvoidingView is enabled or disabled
    3. link
       > https://reactnative.dev/docs/keyboardavoidingview
