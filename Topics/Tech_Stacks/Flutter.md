# Learning Flutter

## Table of contents

#### [What is Flutter](#what-is-flutter)

#### [Creating your first flutter app](#creating-your-first-flutter-app)

## What is Flutter?

Flutter is an open source framework developed and supported by Google. Frontend and full-stack developers use Flutter to build an application’s user interface (UI) for multiple platforms with a single codebase.

Flutter now supports application development on six platforms: iOS, Android, the web, Windows, MacOS, and Linux.

Flutter uses the open-source programming language Dart, which was also developed by Google. Dart is optimized for building UIs, and many of Dart’s strengths are used in Flutter.

Source: [Amazon AWS](https://aws.amazon.com/what-is/flutter/)

## Creating your first flutter app

The following is a summary from the offical [Flutter Docs](https://docs.flutter.dev/get-started/).

1. **Install Flutter**
   <ol type = 'a'>

   <li> [Windows](https://docs.flutter.dev/get-started/install/windows) </li>
   b) [macOS](https://docs.flutter.dev/get-started/install/macos)
   c) [Linux](https://docs.flutter.dev/get-started/install/linux)
   d) [ChromeOS](https://docs.flutter.dev/get-started/install/chromeos)

2. **Install an editor**
   While you can use any editor. These instructions are for setting up Flutter on VS Code
   a) Install VS Code for your respective platform. [Installation Link](https://code.visualstudio.com/download).
   b) Open a browser and go to the [Flutter extension page](https://marketplace.visualstudio.com/items?itemName=Dart-Code.flutter) on the Visual Studio Marketplace.
   c) Click Install. Installing the Flutter extension also installs the Dart extension.

3. **Create the app**
   a) Invoke **View > Command Palette**. This can be done with `ctrl shift p` on Windows or `cmd shift p` on Mac.
   b) Type "flutter", and select the **Flutter: New Project**
   c) Select **application**
   d) Create or select the parent directory for the new project folder.
   e) Enter a project name, such as `my_app`, and press **Enter**.
   f) Wait for project creation to complete and the `main.dart` file to appear.
   The above commands create a Flutter project directory called my_app that contains a simple demo app that uses [Material Components](https://m3.material.io/components).
4. **Running the App**
   a) Locate the VS Code status bar (the blue bar at the bottom of the window).
   b) Select a device from the Device Selector area.
   c) Invoke **Run > Start Debugging** or press `F5`.
   d) Wait for the app to launch—progress is printed in the Debug Console view.
   e) After the app build completes, you’ll see the starter app on your device.
