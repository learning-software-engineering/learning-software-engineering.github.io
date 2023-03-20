# Building Apple Native Software Using Swift and SwiftUI
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

## Testing Your App
Xcode has [built-in simulators for many Apple devices](https://developer.apple.com/documentation/xcode/running-your-app-in-simulator-or-on-a-device)
you can use to run your code and see how it performs. You can also download new simulators for specific a device and operating system version to test
different scenarios, such as an iPhone 11 running iOS 13.

If you have your own Apple device, you can also connect it to your Mac device and run your app on it for testing. Note that as of iOS 14, from your device, you will have to first go to `Settings` > `Privacy & Security` > `Developer Mode` first to allow your device to run apps downloaded from Xcode.
