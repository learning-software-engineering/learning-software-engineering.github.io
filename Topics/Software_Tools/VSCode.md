# Software Engineer's Introduction to Visual Studio Code

## Table of Contents:
- [Software Engineer's Introduction to Visual Studio Code](#software-engineers-introduction-to-visual-studio-code)
  - [Table of Contents:](#table-of-contents)
  - [Introduction](#introduction)
  - [Installation and Setup](#installation-and-setup)
  - [Top Features](#top-features)
    - [IntelliSense](#intellisense)
    - [Debugging with VS Code](#debugging-with-vs-code)
    - [Integrated Terminal](#integrated-terminal)
  - [Extensions](#extensions)
  - [Tips and Tricks](#tips-and-tricks)
  - [Closing Remarks](#closing-remarks)
  - [Additional Resources](#additional-resources)
---

## Introduction
[Microsoft Visual Studio Code](https://code.visualstudio.com/) is a free and lightweight yet powerful code editor popular for its versatility, user-friendly interface, and extensibility. 
VS Code meets the diverse needs of software engineers across different languages and frameworks and offers a variety of features to boost programmer productivity, whether you’re an experienced software engineer or a student starting the journey. 
In this article, we will go over the installation and setup, and explore features like debugging, git integration, and extensions, that make VS Code an all-in-one editor.

## Installation and Setup
Clicking on [this](https://code.visualstudio.com/download) link will take you to the download page where you will be able to select your operating system and download the latest version. 
After the download is complete, you can open the downloaded file to launch the installer and follow the instructions. 
Once you have completed the installation and launch VS Code, you will be greeted by the following screen. 
So, let the adventure begin.

<img width="850" src="https://github.com/parthvats02/learning-software-engineering.github.io/assets/81998163/bce65647-4a2c-40ec-8bef-84ef40209cfb">

## Top Features

### [IntelliSense](https://code.visualstudio.com/docs/editor/intellisense)
An umbrella term for various code editing features, IntelliSense simplifies the coding process by providing code completion, syntax highlighting, Code Actions, and parameter info, among many other useful features.

- Python context-aware code completion recommendation
  <img width="850" src=""> 

- Syntax highlight, enhancing code readability
  <img width="850" src=""> 

- Code Actions
  <img width="850" src=""> 

- Parameter information
  <img width="850" src=""> 

These editing features work together to simplify your coding experience. You can learn more about IntelliSense [here](https://code.visualstudio.com/docs/editor/intellisense).


### [Debugging](https://code.visualstudio.com/docs/editor/debugging) with VS Code
VS Code’s in-built debugger provides a robust and seamless debugging experience. 
It allows you to easily set breakpoints and use the debugger interface to step through and examine the execution (including the variables and the stack) thoroughly.

<img width="350" src="https://github.com/parthvats02/learning-software-engineering.github.io/assets/81998163/98ff90c0-8a63-4544-9d9b-236db6aebfb3"> 

Depending on the language you are using, when you run the debugger, you will be prompted to select or install the debugger for that language. 
Once selected, you will be well-equipped to find those pesky bugs that have been hiding in plain sight!

The debugger’s intuitive and easy-to-use interface allows you to set breakpoints by clicking beside the line number and investigate the state of the execution. 

<img width="350" src="https://github.com/parthvats02/learning-software-engineering.github.io/assets/81998163/322fd5b3-18d9-4e35-be00-14441786dd94"> 

Here is a short video that shows the debugging process for a small Python program using the VS Code debugger:

https://github.com/parthvats02/learning-software-engineering.github.io/assets/81998163/601d30c2-fd2f-4a97-af37-34d786eddf36

The debugger also offers a variety of breakpoint options including but not limited to conditional (only breakpoint), function (easily select functions to breakpoint on), and even in-line breakpoints (breakpoints that let you control the flow of execution up to the granular level). 
You can find these breakpoints and other debug-related settings by going under the Run menu and clicking New Breakpoint (on both Windows and Mac).

<img width="450" src="https://github.com/parthvats02/learning-software-engineering.github.io/assets/81998163/8d2899f4-903a-4c71-a53d-ec0b2b335ea6"> 

If you’re interested in learning more about the debugger, you can check out [this](https://code.visualstudio.com/docs/editor/debugging) debugging guide by VS Code.


### [Integrated Terminal](https://code.visualstudio.com/docs/terminal/basics)

Another powerful feature that VS Code provides is the integrated terminal. 
Whether you’re running *make* commands to build your project or using git through the command line, having access to the terminal inside the editor simplifies the experience and eliminates the need to alternate between the terminal and the code editor. 
To get started with the terminal, simply select the Terminal menu at the top and click New Terminal (on both Windows and Mac).

<img width="450" src="https://github.com/parthvats02/learning-software-engineering.github.io/assets/81998163/182b5066-5a42-48fc-868a-2374a0e9de3c"> 

Whether you choose to use the default terminal or install another one of your preference, you will have access to all the features that the terminal has to offer.

- On the left side of the command, you can see the exit status of the command. Clicking the status, you get options like rerunning the command, copying the output, and so on.

  <img width="650" src="https://github.com/parthvats02/learning-software-engineering.github.io/assets/81998163/a3d5f2eb-c40a-4459-9171-c4c0fd4a3e02"> 
  <img width="450" src="https://github.com/parthvats02/learning-software-engineering.github.io/assets/81998163/d20e66a0-882a-456c-85f6-79bea3c1116c"> 
  <img width="350" src="https://github.com/parthvats02/learning-software-engineering.github.io/assets/81998163/c80a4b62-52aa-48e3-89d3-4855c795218a"> 

- You also have the ability to split terminals, open multiple terminals simultaneously in an organized manner, and keep track of them without the hassle of switching between countless windows. Depending on your machine, you will see relevant options when you click the + sign in the terminal window to run other terminals like Git Bash (if you have it installed).

  <img width="350" src="https://github.com/parthvats02/learning-software-engineering.github.io/assets/81998163/2661f205-055f-40f1-90ed-8b14e9fa969c"> 
  <img width="350" src="https://github.com/parthvats02/learning-software-engineering.github.io/assets/81998163/63bc9d5c-6409-4667-85c3-bf11388cd022"> 

To learn more about the integrated terminal and the features it offers, check out the detailed introduction by VSCode [here](https://code.visualstudio.com/docs/terminal/basics).


## Extensions
Extensions are a big part of the Visual Studio Code ecosystem as they make the editor even more powerful. 
Extensions include everything ranging from languages and debuggers to tools and customizers that allow you to have all that you need in your development workflow.

To get started with extensions, click the four squares (building blocks) icon in the left pane. 
Be cautious as this may open the doors to countless options that help you tailor VS Code to your workflow!

<img width="350" src="https://github.com/parthvats02/learning-software-engineering.github.io/assets/81998163/a4e4382c-5f4a-402c-af73-260fd3a10e96"> 

No matter the language or framework you are working with, Extensions has you covered. 
Simply search what you are looking for in the search bar and you will see numerous results to choose from. 

Here are a few popular categories and extensions that you have access to:

- Debuggers extensions like the Python and JavaScript Debugger to help you find the hard-to-find bugs.
  <img width="250" src="https://github.com/parthvats02/learning-software-engineering.github.io/assets/81998163/25eb6236-3057-4a25-b2e2-83a589ed9afa"> 

- Language tools including IntelliSense extensions to tailor the editor specifically to the language you are using.

- Linters and formatters to ensure your code is well-formatted and easy to read.

- Database extensions, ranging from PostgreSQL to MongoDB, that elevate your database interactions by providing custom tools and a better database user interface.

- Container extensions like Docker which allows you to inspect the containers, images, registries and more during execution.
  
  <img width="450" src="https://github.com/parthvats02/learning-software-engineering.github.io/assets/81998163/994fc120-155c-4a5c-9351-f82e2afb905f"> 

- Git-related extensions like GitLens which supercharges your git powers, and allows you to inspect file commit history, display the last modifier in-line (useful when investigating where a breaking change got introduced), and much more within a few clicks.
  
  <img width="450" src="https://github.com/parthvats02/learning-software-engineering.github.io/assets/81998163/5fef0170-6925-4e31-a467-abff4e19a625"> 

- Themes that enable you to customize VS Code exactly as you want it.

- And many more extensions. You can find other categories by clicking the filter icon in the extension search bar and selecting Category.
  
  <img width="550" src="https://github.com/parthvats02/learning-software-engineering.github.io/assets/81998163/8eb00778-24b3-4b9d-8a79-43ad40050c02"> 

Feeling excited and love to learn more about extensions? Check out [this](https://code.visualstudio.com/docs/editor/extension-marketplace) detailed page by VSCode to get started.


## Tips and Tricks
With an editor so powerful comes a myriad of tips and tricks to improve your experience. 
Here are some quick hand-picked tips and tricks:

- You can split the editor by clicking the icon here which allows you to work with your files at multiple locations simultaneously
  
  <img width="350" src="https://github.com/parthvats02/learning-software-engineering.github.io/assets/81998163/0878cfc5-0b4d-44fa-8d0f-1d0ab85370fe"> 

- You can enable Zen Mode (by clicking View -> Appearance -> Zen Mode) to reduce distractions and focus only your code, and can disable it by pressing Escape on your keyboard twice
  <img width="550" src="https://github.com/parthvats02/learning-software-engineering.github.io/assets/81998163/cd2b30a3-ca30-4dc4-b1ed-dfbd5b9ab8f5"> 

- You can use and modify keyword shortcuts to simplify your workflow. Image below by VSCode from Visual Studio Code Tips and Tricks (https://code.visualstudio.com/docs/getstarted/tips-and-tricks)
  <img width="650" src="https://github.com/parthvats02/learning-software-engineering.github.io/assets/81998163/d893293e-a381-4d3d-a72c-e006d0fdbdc3"> 

For an extensive list of tips and tricks, visit the official [Visual Studio Code Tips and Tricks page](https://code.visualstudio.com/docs/getstarted/tips-and-tricks) to supercharge your VS Code experience.


## Closing Remarks

This article only scratches the surface and there is a whole world to explore with Visual Studio Code that could not be fully tapped into in this article. 
To learn more about VS Code, be sure to check out the Additional Resources section for more information. 
Superpowers await you on the other side, what are **you** waiting for?


## Additional Resources

Official Visual Studio Code documentation and user guide: https://code.visualstudio.com/docs

Official Visual Studio Code YouTube channel with numerous playlists: https://www.youtube.com/@code

Learn to code with Visual Studio Code: https://code.visualstudio.com/learn

Visual Studio Code in 100 Seconds: https://www.youtube.com/watch?v=KMxo3T_MTvY


