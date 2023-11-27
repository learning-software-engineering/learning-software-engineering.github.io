# Learning Flutter

## Table of contents

#### [What is Flutter](#what-is-flutter)

#### [Why Flutter? Pros and Cons](#why-flutter-pros-and-cons)

#### [Creating your first flutter app](#creating-your-first-flutter-app)

## What is Flutter?

Flutter is an open source framework developed and supported by Google. Frontend and full-stack developers use Flutter to build an application’s user interface (UI) for multiple platforms with a single codebase.

Flutter now supports application development on six platforms: iOS, Android, the web, Windows, MacOS, and Linux.

Flutter uses the open-source programming language Dart, which was also developed by Google. Dart is optimized for building UIs, and many of Dart’s strengths are used in Flutter.

Source: [Amazon AWS](https://aws.amazon.com/what-is/flutter/)

Many companies use Flutter to build their applications. Some of these companies include: Alibaba Group, Tencent, BMW and many more. For a full list of companies that use Flutter, click [here](https://flutter.dev/showcase).

## Why Flutter? Pros and Cons

### Pros:

1. **Single codebase for all platforms**
   There is no need to create separate code bases when working on iOS and Android devices. Flutter allows developers to build a single codebase and use it for several platforms such as the web, desktop and mobile. This results in quicker app launch and is cost effective.
2. **Reduced Development Time**
   The requirements for Flutter application development are much lower. So the positive outcome is that there are no additional maintenance charges. Flutter makes it possible to create larger apps that use unique features.
3. **Hot Reload Feature**
   The ability to hot reload is one of the main benefits of using Flutter. This is for effective cross-platform development so it can complement the nature of Flutter. This feature’s function speeds up application development. Hot reloading allows developers to see the changes they make to the code in real time without losing the state of the app. It is useful when editing the UI of an app.

### Cons:

1. **Dart’s low popularity**
   It’s a fact that Dart is a reliable programming language since it is fast. It is also true that developers are starting to make it an option. Yet, Dart is still not able to compete with other top programming languages such as Java, Kotlin, etc. However Dart is very similar to C# and Java, which makes it easy for programmers to learn.
2. **Large and Weighty Apps**
   A loophole that can’t be dismissed is the size of the large size of the applications under development. Software developers working with this toolkit may find it difficult to work with large files. This can cause them to choose a lighter alternative.
3. **Limited number of third-party libraries**
   Flutter being relatively new cannot be compared to native programming languages. Developers still need to spend more time building as many libraries as possible.

   Source [Waverley Software](https://waverleysoftware.com/blog/why-use-flutter-pros-and-cons/#:~:text=Flutter%20allows%20developers%20to%20build,application%20development%20are%20much%20lower.)

## Creating your first flutter app

The following is a summary from the offical [Flutter Docs](https://docs.flutter.dev/get-started/).

1. **Install Flutter**

   1. [Windows](https://docs.flutter.dev/get-started/install/windows)
   2. [macOS](https://docs.flutter.dev/get-started/install/macos)
   3. [Linux](https://docs.flutter.dev/get-started/install/linux)
   4. [ChromeOS](https://docs.flutter.dev/get-started/install/chromeos)

2. **Install an editor**
   While you can use any editor. These instructions are for setting up Flutter on VS Code

   1. Install VS Code for your respective platform. [Installation Link](https://code.visualstudio.com/download).
   2. Open a browser and go to the [Flutter extension page](https://marketplace.visualstudio.com/items?itemName=Dart-Code.flutter) on the Visual Studio Marketplace.
   3. Click Install. Installing the Flutter extension also installs the Dart extension.

3. **Create the app**

   1. Invoke **View > Command Palette**. This can be done with `ctrl shift p` on Windows or `cmd shift p` on Mac.
      <img width="636" alt="VS Code Command Palette" src="https://github.com/learning-software-engineering/learning-software-engineering.github.io/assets/65613404/9bdf3ef1-ad9b-4848-b6bb-723f85462c36">
   2. Type "flutter", and select the **Flutter: New Project**
      <img width="644" alt="Flutter new project" src="https://github.com/learning-software-engineering/learning-software-engineering.github.io/assets/65613404/47cf0a8d-25a5-4076-ad6d-54cc8197384d">
   3. Select **application**
   4. Create or select the parent directory for the new project folder.
   5. Enter a project name, such as `my_app`, and press **Enter**.
   6. Wait for project creation to complete and the `main.dart` file to appear.
      The above commands create a Flutter project directory called my_app that contains a simple demo app that uses [Material Components](https://m3.material.io/components).
   7. Your file structures should look as follows. <br>
      <img width="197" alt="Final File Structure" src="https://github.com/learning-software-engineering/learning-software-engineering.github.io/assets/65613404/11b6c999-a556-452c-867f-9299a6cef3b1">

4. **Running the App**
   1. Locate the VS Code status bar (the blue bar at the bottom of the window).
   2. Select a device from the Device Selector area.
   3. Invoke **Run > Start Debugging** or press `F5`.
   4. Wait for the app to launch—progress is printed in the Debug Console view.
   5. After the app build completes, you’ll see the starter app on your device.
