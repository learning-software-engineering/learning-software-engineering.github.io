# Building Apple Native Software Using Swift and SwiftUI

## Table of contents
### [Introduction](#introduction-1)
### [Why Use Swift?](#why-use-swift-1)
### [What is SwiftUI?](#what-is-swiftui-1)
### [Starting a Swift Project](#starting-a-swift-project-1)
### [Testing Your App](#testing-your-app-1)
### [Other Useful Resources](#other-useful-resources-1)

## Introduction
Swift is a modern, open-source programming language developed by Apple as a replacement to their earlier language, Objective-C.

It can be used on Mac devices to develop software that target all Apple platforms: iOS, macOS, watchOS, and tvOS, while being deeply
integrated into Apple's IDE: Xcode.

In the following official Apple documentation, there are many other resources, such as videos, interactive demos, and guided
exercises, you can use to better understand and practice these tools.

[Swift Getting Started Documentation](https://www.swift.org/getting-started/)

[SwiftUI Documentation](https://developer.apple.com/documentation/swiftui/)

[Xcode Documentation](https://developer.apple.com/documentation/xcode)

## Why Use Swift?
While languages such as React Native allow you to build multi-platform apps, such as for iOS and Android, using only one source code,
Swift offers many tools that make it easy to quickly build apps that work specifically throughout all of Apple's ecosystem of platforms.

Apps built through Swift can intuitively [support iPhone and iPad screens at the same time](https://developer.apple.com/news/?id=nixcb564),
utilizing design patterns and themes that fit Apple's design policy to match the expected user experience on an iOS device.

You will have access to an [assortment of developer kits](https://developer.apple.com/documentation/technologies?input=kit) that make
it simpler to integrate various, native features into your app. For example, [WidgetKit](https://developer.apple.com/documentation/WidgetKit)
can help set up widgets for iOS Home Screens for your app, or [HealthKit](https://developer.apple.com/documentation/healthkit) can allow you
to communicate to a user's health and fitness data, with their permission.

It comes built-in with over 4000 customizable icons and symbols that are designed to seamlessly match Apple software, which you can view and
modify through [SF Symbols 4](https://developer.apple.com/sf-symbols/).

These are just some of the many advantages available.

## What is SwiftUI?
In 2019, Apple introduced a new framework for building user interfaces called SwiftUI. This is a [declarative UI toolkit](https://www.hackingwithswift.com/quick-start/swiftui/what-is-swiftui), similar to React, where we can tell it what components we want
and the framework will handle performing the steps needed to get that result.

[Hacking with Swift](https://www.hackingwithswift.com) is a great free resource for learning how to do specific things in Swift and SwiftUI
when the issues arise.

## Starting a Swift Project
After launching Xcode, selecting `Create a new Xcode project`, and choosing which platform and type of app you want to make, you will then have
to fill in the following info:

<img width="1512" alt="Screen Shot 2023-03-20 at 4 31 06 PM" src="https://user-images.githubusercontent.com/65694861/226458997-0d9c6227-9ce6-4d34-91b0-58c69b02d016.png">

This information can be changed later, so for starters you can leave `Team` to be empty, as this is only necessary for deploying the app to the App Store. `Organization identifier` is used to uniquely identify your app once it is up on the App Store, so you can choose whichever name you'd like, such as your name or group's name. Do note `Organization identifier` cannot be changed once the app is uploaded to the App Store but it is purely meta data.

Make sure to use `SwiftUI` and `Swift` as your interface and language respectively, then click `Next` to choose where to store your project, and now you're ready to start.

## Swift View
A view is a part of a swift application’s user interface. Creating a new project automatically creates a view called content view.  
<img width="283" alt="Screenshot 2023-11-23 at 12 32 33 AM" src="https://github.com/learning-software-engineering/learning-software-engineering.github.io/assets/97854264/58e8197c-897b-4bff-be4d-77b6daa62ecd">
Views in Swift are defined as structs and must conform to the View protocol. The content and behavior of the view are provided in the body of the view. To see how the view is transformed into the user’s interface and how users can interact with the view, we can either build and run our application on a simulated device or view the Xcode preview. Refer to the Testing Your App - Simulators: Background section to set up the simulator. An Xcode preview is created by the code defined in lines 22 - 24. It generates a view preview without having to build and run the app. When we open up our project, the preview will appear, as shown below, displaying the view.
<img width="472" alt="Screenshot 2023-11-23 at 12 34 28 AM" src="https://github.com/learning-software-engineering/learning-software-engineering.github.io/assets/97854264/93913afd-a6df-4958-a1e6-d7fe276814ea">

**Editing a View**

We can edit a view in two ways: manually or through the view inspector. Modifications to the view’s body will be reelected in real-time in the preview.For our example, we will show how to edit the text colour manually and through a view inspector. To edit a view through an inspector.

1. Change from live mode ( default mode) to selectable mode to enable editing
<img width="357" alt="Screenshot 2023-11-23 at 12 35 23 AM" src="https://github.com/learning-software-engineering/learning-software-engineering.github.io/assets/97854264/0854dc19-a15a-476b-bd4c-ab442d227f50">

2. Command-control-click the element you want to edit, bringing up the structured editing pop-up. The pop-up shows the different attributes you can customize, which attributes to customize depending on the type of view. For our example, we will customize the colour attribute. Select “Show SwiftUI Inspector”.
<img width="252" alt="Screenshot 2023-11-23 at 12 35 54 AM" src="https://github.com/learning-software-engineering/learning-software-engineering.github.io/assets/97854264/9f115e5b-7773-44e3-9e4b-48366bf54d2f">

3. Select the color attribute and choose the color purple.
<img width="351" alt="Screenshot 2023-11-23 at 12 36 25 AM" src="https://github.com/learning-software-engineering/learning-software-engineering.github.io/assets/97854264/b6a04517-1aba-4dea-9b41-099aa592295b">

The change will be reflected immediately on the simulated device, and Xcode will update your code to match the change. 
<img width="528" alt="Screenshot 2023-11-23 at 12 36 48 AM" src="https://github.com/learning-software-engineering/learning-software-engineering.github.io/assets/97854264/2514b9b0-1516-4783-a78e-9de37226d6f3">
To edit manually, we must add the line “foregroundColor (Color.purple)” to the view’s body.

**Previewing Light and Dark Modes, Orientations, and Device Types**

We can see how our user interface will look in light and dark modes. Select the variant control and “Colour Scheme Variants” to do so.
<img width="528" alt="Screenshot 2023-11-23 at 12 39 27 AM" src="https://github.com/learning-software-engineering/learning-software-engineering.github.io/assets/97854264/d0c765f1-5fce-4c88-993b-729a8d9b612d">
<img width="527" alt="Screenshot 2023-11-23 at 12 39 44 AM" src="https://github.com/learning-software-engineering/learning-software-engineering.github.io/assets/97854264/eb34957e-5e9c-4ff6-9554-d8c8de007eb0">
We can also view how the user interface will look in different orientations by selecting the “Orientation Variant.”
<img width="530" alt="Screenshot 2023-11-23 at 12 40 07 AM" src="https://github.com/learning-software-engineering/learning-software-engineering.github.io/assets/97854264/2ca289f4-b042-4abc-8720-56566890dc9e">
To view the preview on different device types, you can change the device the preview is displayed on from the buttons below. Here is an example of the same view shown on an iPad.
<img width="529" alt="Screenshot 2023-11-23 at 12 40 28 AM" src="https://github.com/learning-software-engineering/learning-software-engineering.github.io/assets/97854264/eedb61c6-47fd-4a0e-8d73-b5e8f8b1f287">



## Testing Your App
Xcode has [built-in simulators for many Apple devices](https://developer.apple.com/documentation/xcode/running-your-app-in-simulator-or-on-a-device)
you can use to run your code and see how it performs. You can also download new simulators for specific a device and operating system version to test
different scenarios, such as an iPhone 11 running iOS 13.

If you have your own Apple device, you can also connect it to your Mac device and run your app on it for testing. Note that as of iOS 14, from your device, you will have to first go to `Settings` > `Privacy & Security` > `Developer Mode` first to allow your device to run apps downloaded from Xcode.


## Other Useful Resources
[Learn about the different data types in Swift](https://www.hackingwithswift.com/read/0/3/types-of-data). Each language has its own nuances in how
variables are declared and stored, useful to become familiar with it before starting to code.

[SwiftUI has many property wrappers that provide different functionality to the object instances they are attached to](https://www.hackingwithswift.com/quick-start/swiftui/all-swiftui-property-wrappers-explained-and-compared). These are an important tool for making your code efficient and storing your objects properly. In particular, you should be aware of what the `@State` and `@Binding` wrappers do.

[Learn about Protocols for defining properties object models must have](https://www.hackingwithswift.com/read/0/22/protocols). These function similar to what are known as `Interfaces` in other languages. Protocols are important as you will sometimes run into errors that require the object you are using to "conform" to some protocol. For example, if you are trying to loop over a custom object, you must first have that object [conform to Identifiable](https://www.hackingwithswift.com/quick-start/swiftui/how-to-fix-initializer-init-rowcontent-requires-that-sometype-conform-to-identifiable) so that Swift can iterate through a list of that object and recognize which entries are unique.
