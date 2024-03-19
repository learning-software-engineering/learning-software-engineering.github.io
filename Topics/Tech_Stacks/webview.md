# Open website in IOS or Android using Webview.


## Introduction

As the use of mobile devices continues to grow, many websites are now being accessed through mobile apps instead of traditional web browsers. To provide a seamless user experience, developers often use a WebView component in their iOS or Android app to open a website within the app. A WebView is a user interface component that displays web content within an application. By using a WebView, developers can embed web content, such as web pages or online services, directly into their mobile app, without the need to switch between the app and a separate web browser. In this way, users can stay within the app and seamlessly interact with web content. This approach has become increasingly popular in the development of mobile apps, especially for those that need to integrate web-based content into their user interface.
## Emulator

https://snack.expo.dev/
This link provide an emulator for mobile, you don't have to download anything. Remember to save your changes and bookmark the webpage. On the right side, you can see iOS and Android. Click them and click tap to play, it will install the app you created in an emulator and open that app for you.

## package.json

Include all the package you need in package.json
```cpp
{
  "dependencies": {
    "expo-constants": "~13.2.4",
    "@expo/vector-icons": "^13.0.0",
    "react-native-paper": "4.9.2",
    "react-native-webview": "11.23.0"
  }
}
```

## App.js

This is where you put your code in. 
```cpp
import React, { useState, useRef } from 'react';
import { WebView } from 'react-native-webview';
import { Button } from 'react-native';
import { View } from 'react-native';

export default function App() {
  const [showWebView, setShowWebView] = useState(false);
  const webViewRef = useRef(null);

  const openWebView = () => {
    setShowWebView(true);
  };

  const closeWebView = () => {
    setShowWebView(false);
  };

  return (
    <View style={{ flex: 1 }}>
      {showWebView ? (
        <>
          <WebView
            ref={webViewRef}
            source={{ uri: 'https://google.ca' }}
            style={{ flex: 1 }}
          />
          <Button title="Close" onPress={closeWebView} />
        </>
      ) : (
        <View style={{ flex: 1, justifyContent: 'center' }}>
          <Button title="Open Google" onPress={openWebView} />
        </View>
      )}
    </View>
  );
}

```
Please try this code yourself and play around with it. It creates an app that has a button called "Open Google" in the middle. If you click that button, the Google website will open using a WebView component within the app. You can close it by clicking the close button at the bottom of the WebView window. You can change the website to whatever you want. You can even ask ChatGPT to modify it.
