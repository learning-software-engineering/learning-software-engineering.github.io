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

<img width="850" alt="VSCode New" src="https://github.com/parthvats02/learning-software-engineering.github.io/assets/81998163/bce65647-4a2c-40ec-8bef-84ef40209cfb">

## Top Features

### [IntelliSense](https://code.visualstudio.com/docs/editor/intellisense)
An umbrella term for various code editing features, IntelliSense simplifies the coding process by providing code completion, syntax highlighting, Code Actions, and parameter info, among many other useful features.

[Picture 1] Python context-aware code completion recommendation

[Picture 2] Syntax highlight, enhancing code readability

[Picture 3] Code Actions

[Picture 4] Parameter information

These editing features work together to simplify your coding experience. You can learn more about IntelliSense [here](https://code.visualstudio.com/docs/editor/intellisense).


### [Debugging](https://code.visualstudio.com/docs/editor/debugging) with VS Code
VS Code’s in-built debugger provides a robust and seamless debugging experience. 
It allows you to easily set breakpoints and use the debugger interface to step through and examine the execution (including the variables and the stack) thoroughly.


Depending on the language you are using, when you run the debugger, you will be prompted to select or install the debugger for that language. 
Once selected, you will be well-equipped to find those pesky bugs that have been hiding in plain sight!

The debugger’s intuitive and easy-to-use interface allows you to set breakpoints by clicking beside the line number and investigate the state of the execution. 


Here is a short video that shows the debugging process for a small Python program using the VS Code debugger:


The debugger also offers a variety of breakpoint options including but not limited to conditional (only breakpoint), function (easily select functions to breakpoint on), and even in-line breakpoints (breakpoints that let you control the flow of execution up to the granular level). 
You can find these breakpoints and other debug-related settings by going under the Run menu and clicking New Breakpoint (on both Windows and Mac).


If you’re interested in learning more about the debugger, you can check out [this](https://code.visualstudio.com/docs/editor/debugging) debugging guide by VS Code.


### [Integrated Terminal](https://code.visualstudio.com/docs/terminal/basics)

Another powerful feature that VS Code provides is the integrated terminal. 
Whether you’re running *make* commands to build your project or using git through the command line, having access to the terminal inside the editor simplifies the experience and eliminates the need to alternate between the terminal and the code editor. 
To get started with the terminal, simply select the Terminal menu at the top and click New Terminal (on both Windows and Mac).



Whether you choose to use the default terminal or install another one of your preference, you will have access to all the features that the terminal has to offer.

- On the left side of the command, you can see the exit status of the command. Clicking the status, you get options like rerunning the command, copying the output, and so on.

- You also have the ability to split terminals, open multiple terminals simultaneously in an organized manner, and keep track of them without the hassle of switching between countless windows. Depending on your machine, you will see relevant options when you click the + sign in the terminal window to run other terminals like Git Bash (if you have it installed).

To learn more about the integrated terminal and the features it offers, check out the detailed introduction by VSCode [here](https://code.visualstudio.com/docs/terminal/basics).






