1. React Native

   1. Set up
      1. Installation
         1. Install Node.js and npm (Node Package Manager) on your computer. You can download and install Node.js from the official website: https://nodejs.org/en/
            #Note: Suggested to download the LTS version because it is generally more stable than the Current or Latest version.
         2. Install expo go on your ios device (https://apps.apple.com/us/app/expo-go/id982107779) or android device (https://play.google.com/store/apps/details?id=host.exp.exponent&hl=en_CA&gl=US&pli=1)
         3. Download VS Code Extensions
            1. ES7+ React/Redux/React-Native snippets (Extension ID: dsznajder.es7-react-js-snippets)
            2. React Native Tools (Extension ID: msjsdiag.vscode-react-native)
      2. Command
         1. Install expo
            `npm install -g expo-cli`
         2. Initialize expo
            `expo init your_app_name`
            #Note: you will be able to choose "blank", "blank (TypesScript)", "tabs (TypeScript)", or "minimal". I personally prefer blank because often times I need to delete files I don't want.
         3. Start expo
            `cd your_app_name`
            `expo start`
      3. Running expo
         1. Phone
            Open the expo go app and scan the QR Code after the "`expo start`" command
            #Note: you can shake your phone or put three fingers on the screen to restart the app without closing the app and reopening it.
         2. Emulator on PC
            1. macOS
               You can try to use Xcode on your mac device and see live changes without using a mobile device
            2. Windows
               You can run an ios emulator or android emulator using the React Native Tools installed earlier
   2. [Common React Native Components](./React_Native_Component.md)  
      This guide provides an overview of commonly-used React Native components for mobile app development.
