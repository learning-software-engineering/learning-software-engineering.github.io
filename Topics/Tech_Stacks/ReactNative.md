# React Native
## Developing a Mobile App with Expo

React Native is a convenient JavaScript framework created by Meta Platforms Inc. for developing applications. Specifically, its ability to natively render mobile applications on both iOS and Andriod platforms. In addition to its cross-platform functionality, it is primarily based off of React, allowing programmers to immigrate to this framework at ease. Furthermore, React Native is an open-source framework that consists of numerous libraries to assist your application development. <br>

Before my CSC301 advanture, I had no basics in React nor React Native. However, React Native is not a tough framework to learn, so don't stress out and feel free to dive into the [basic documentations](https://reactnative.dev/docs/tutorial) and [beginner courses](https://www.codecademy.com/learn/learn-react-native)! Many [interactive examples](https://reactnative.dev/docs/getting-started) are provided by the developers for you to test and play around with.

Meanwhile, [EXPO](https://docs.expo.dev) is a open-source platform built around React Native. It contains a series of useful tools for developing a React Native app. This includes convenient commands to create and test your app universally on iOS, Android and web without additional configuration. Hence, it is highly recommended to use Expo if you are beginning the development of a mobile app. Furthermore, even existing React Native apps can have the `expo` package installed. <br>

With Expo's [EAS Update](https://docs.expo.dev/eas-update/introduction/) and [EAS Build](https://docs.expo.dev/build/introduction/) features, development builds can be launched instantly, and your app can be tested on mobile devices or mobile device simulators. Official builds can also be launched efficiently to share among your team, or even make its way to AppStore and Google Play. Additionally, Expo offers a [web dashboard](https://expo.dev) with concise UI that aids the management of projects and their deployment. You can sign up for a free Expo account and manage your projects on this dashboard. The [Expo-CLI](https://docs.expo.dev/more/expo-cli/) is the command-line tool that connects all these tools together, and even helps to securely manage your project's dependencies.<br>

   1. Set up
      1. Installation
         1. Install Node.js and npm (Node Package Manager) on your computer. You can download and install Node.js from the official website: https://nodejs.org/en/
            #Note: Suggested to download the LTS version (or even numbered versions npm) because it is generally more stable. Use `npm -v` and `Node -v` to check your installed version.
         2. Install Expo Go on your [iOS device](https://apps.apple.com/us/app/expo-go/id982107779) or [Android device](https://play.google.com/store/apps/details?id=host.exp.exponent&hl=en_CA&gl=US&pli=1) via App Store and Google Play Store
         3. Download VS Code Extensions
            1. ES7+ React/Redux/React-Native snippets (Extension ID: dsznajder.es7-react-js-snippets)
            2. React Native Tools (Extension ID: msjsdiag.vscode-react-native)
      2. Command
         1. Install Expo CLI (command line tool)
            `npm install -g expo-cli`
         2. Initialize expo
            `expo init <your_app_name>`
            #Note: you will be able to choose "blank", "blank (TypesScript)", "tabs (TypeScript)", or "minimal". I personally prefer blank because often times I need to delete files I don't want.
         3. Start expo
            `cd <your_app_name>`
            `npx expo start`
            A development build will be launched
         4. Installing Dependencies
         `npx expo install <library-name>` or `npx expo install` to install libraries to local repository specified in `package.json`
            1. Useful dependencies:
               1. `react-native-web` and `@expo/webpack-config` -- to run your development on a web browser
               2. `jest` and `jest-expo` -- Useful react Native testing packages. Extra configurations need to be made in your project, for more details see [Expo Unit Testing Documentation](https://docs.expo.dev/develop/unit-testing/) and [guide](../Development_Process/React_Testing_Library.md)
               3. [`react-navigation`](./React_Navigation.md) -- Handy library to manage navigation between different screens in your app
               4. [`axios`](./Axios.md) -- A great library to make HTTP requests for connecting your front-end to a back-end server
      3. Running expo
         1. Phone
            Scan the QR Code from running the "`npx expo start`" command. For iOS device, scan using your phone's default camera and it will automatically redirect you to the Expo Go App, and Android devices can scan the QR code using the Expo Go app.
            #Note: you can shake your phone or put three fingers on the screen to restart the app without closing the app and reopening it.
         2. Emulator on PC
            1. macOS
               You can try to use Xcode on your mac device and see live changes without using a mobile device
            2. Windows
               You can run an ios emulator or android emulator using the React Native Tools installed earlier
         3. With the relative dependencies installed, press 'w' to open a web browser to view your development build
         4. Press 'j' to open a debugger. Here is a [detailed guide](./swift.md) on how to debug your application
   2. [Common React Native Components](./React_Native_Component.md)  
      This guide provides an overview of commonly-used React Native components for mobile app development.
   3. Managing Dependencies
      As your project grows, your list of dependencies will inevitably grow. To ensure a tidy workspace for you and everyone on the team, it is a good practise to keep a clean dependency list and locally installed libraries. In any React Native App, there is a `package.json` file that keeps a list of the required dependencies (and their version), and a `package-lock.json` file that ensures  installations by locking the exact versions of dependencies. These two files are crucial must be in-sync for the team, so make sure always have the correct version of it on everyone's branch, and remove redundant dependencies. Therefore, I suggest having a specific branch to manage the dependencies to make sure everyone on the team are using the same versions of each library, and to avoid conflicts. Meanwhile, the locally installed libraries are in the `node_modules` directory, and does ***not*** need to be committed unless for special needs. All team members updating their local repository should simply run `npx expo install` when their `package.json` is up-to-date. FYI, `node_modules` and `.expo` directories are automatically in `.gitignore` if you created the project using Expo.
