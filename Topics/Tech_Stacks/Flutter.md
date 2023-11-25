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
   2. Type "flutter", and select the **Flutter: New Project**
   3. Select **application**
   4. Create or select the parent directory for the new project folder.
   5. Enter a project name, such as `my_app`, and press **Enter**.
   6. Wait for project creation to complete and the `main.dart` file to appear.
      The above commands create a Flutter project directory called my_app that contains a simple demo app that uses [Material Components](https://m3.material.io/components).
4. **Running the App**
   1. Locate the VS Code status bar (the blue bar at the bottom of the window).
   2. Select a device from the Device Selector area.
   3. Invoke **Run > Start Debugging** or press `F5`.
   4. Wait for the app to launch—progress is printed in the Debug Console view.
   5. After the app build completes, you’ll see the starter app on your device.
