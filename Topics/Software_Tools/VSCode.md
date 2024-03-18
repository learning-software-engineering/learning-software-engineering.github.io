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
  - [Working with GitHub through VS Code](#working-with-github-through-vs-code)
    - [Prerequisites](#prerequisites)
    - [Initializing and publishing your local repository to GitHub](#initializing-and-publishing-your-local-repository-to-github)
    - [Cloning a GitHub Repository](#cloning-a-github-repository)
    - [Tracking Changes](#tracking-changes)
    - [Adding files to be committed](#adding-files-to-be-committed)
    - [Committing files](#committing-files)
    - [Pushing and pulling files to and from GitHub](#pushing-and-pulling-files-to-and-from-github)
  - [Closing Remarks](#closing-remarks)
  - [Additional Resources](#additional-resources)
  - [References and Citations](#references-and-citations)
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
An umbrella term for various code editing features, IntelliSense simplifies the coding process by providing code completion, syntax highlighting, Code Actions, and parameter info, among many other useful features. To name a few major ones:

- Python context-aware code completion recommendation
  
  <img width="350" src="https://github.com/parthvats02/learning-software-engineering.github.io/assets/81998163/9d2d39b9-e31d-407a-b17c-ece3f190714c"> 

- Syntax highlight, enhancing code readability
  
  <img width="350" src="https://github.com/parthvats02/learning-software-engineering.github.io/assets/81998163/ac670db1-d7eb-4164-9627-cddfc19196be"> 

- Code Actions

<img width="350" src="https://github.com/parthvats02/learning-software-engineering.github.io/assets/81998163/eadf36f3-6fdf-493d-b087-cd1d380088d4"> 

- Parameter information
  
  <img width="350" src="https://github.com/parthvats02/learning-software-engineering.github.io/assets/81998163/d56b7e99-52a6-4290-8001-83eff5d0aa76"> 

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
  <br>
  <img width="350" src="https://github.com/parthvats02/learning-software-engineering.github.io/assets/81998163/c80a4b62-52aa-48e3-89d3-4855c795218a"> 

  - You also have the ability to split terminals, open multiple terminals simultaneously in an organized manner, and keep track of them without the hassle of switching between countless windows. Depending on your machine, you will see relevant options when you click the + sign in the terminal window to run other terminals like Git Bash (if you have it installed).

  <img width="350" src="https://github.com/parthvats02/learning-software-engineering.github.io/assets/81998163/2661f205-055f-40f1-90ed-8b14e9fa969c"> 
  <img width="341" src="https://github.com/parthvats02/learning-software-engineering.github.io/assets/81998163/63bc9d5c-6409-4667-85c3-bf11388cd022"> 

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
  
  <img width="350" src="https://github.com/parthvats02/learning-software-engineering.github.io/assets/81998163/994fc120-155c-4a5c-9351-f82e2afb905f"> 

- Git-related extensions like GitLens which supercharges your git powers, and allows you to inspect file commit history, display the last modifier in-line (useful when investigating where a breaking change got introduced), and much more within a few clicks.
  
  <img width="350" src="https://github.com/parthvats02/learning-software-engineering.github.io/assets/81998163/5fef0170-6925-4e31-a467-abff4e19a625"> 

- Themes that enable you to customize VS Code exactly as you want it.

- And many more extensions. You can find other categories by clicking the filter icon in the extension search bar and selecting Category.
  
  <img width="450" src="https://github.com/parthvats02/learning-software-engineering.github.io/assets/81998163/8eb00778-24b3-4b9d-8a79-43ad40050c02"> 

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

## Working with GitHub through VS Code

Version control is a system that keeps track of changes to your files so that you can later recall a previous version (https://git-scm.com/book/en/v2/Getting-Started-About-Version-Control). GitHub is one of the most powerful such systems and is a go-to for many team projects like CSC301 because you can collaborate together, see the changes that have been made and you can rollback to a previous working version if something goes wrong. For additional info take a look at this [Git](../Development_Process/Git/Git.md) page in the Software Engineering Learning Center.

One of the most powerful use cases of VS Code is that it has integrated source control management and includes Git support. This means that whenever you are working on a remote repository on GitHub, you can clone, commit and push your code through VSCode conveniently and you can even track the changes you've made which can be very helpful. You can work with GitHub through the integrated terminal as well, and you can also directly work on it with the VS Code UI. This section will show how you can work on GitHub repositories with VS Code. This section is based on the VS Code Docs ["Using Git source control in VS Code"](https://code.visualstudio.com/docs/sourcecontrol/overview), ["Introduction to Git in VS Code"](https://code.visualstudio.com/docs/sourcecontrol/intro-to-git), [Source Control FAQ](https://code.visualstudio.com/docs/sourcecontrol/faq)

### Prerequisites

Git has to be installed on your machine. Check if it has been installed and install it if required.

Sign into GitHub through VS Code. You can do this by going to the Accounts Tab on the left pane and following the process.

### Initializing and publishing your local repository to GitHub

If you are working in your local folder, you might consider making a Git repo in that folder. This could be useful because if you make a change to some code that works and it breaks after the changes, you could easily revert back to the previous working version. You can do this by opening the folder in VS Code and then navigating to the Source Control tab then selecting the "Initialize Repository" button, creates a Git Repository, thereby making it easy to track changes. 

<img width="400" alt="Initialize and publish git repo" src="https://github.com/vazevaru/learning-software-engineering.github.io/assets/90367491/e8c6a30a-c333-4116-bdff-d59112c00765">

If you are working on a local repository and want to publish it to GitHub, you can do this by opening the folder in VS Code and then navigating to the Source Control tab. To then publish this repository to GitHub press the "Publish to GitHub" button, and after selecting a few options to make the repository, you have successfully published your local repo to GitHub!

### Cloning a GitHub Repository

If you want to work on an existing repo on GitHub, then you can clone it to work on it locally in VS Code. To do this, first open a new window in VS Code, you will be greeted with the screen below. Click on “Clone Git repository.” You can also go to the "Explorer" tab or the "Version Control" tab on the left pane and do the same.

<img width="800" alt="Clone Git repo new window" src="https://github.com/vazevaru/learning-software-engineering.github.io/assets/90367491/416d94f7-23f8-467f-af80-d6a622985a78">

This will make a text box appear. 

<img width="800" alt="Clone textbox" src="https://github.com/vazevaru/learning-software-engineering.github.io/assets/90367491/b24e534f-8ff9-4b34-960f-458ce2326869">

You can search for the relevant repository and select it. After selecting it, you need to specify a location for the repo. You can either create a new folder or clone it in an existing folder. After selecting the location, you can open the folder and work on the repo!

<img width="800" alt="Git clone select repo location" src="https://github.com/vazevaru/learning-software-engineering.github.io/assets/90367491/6e6b16e1-05ec-4cf4-987e-3c0e0645bd0b">


### Tracking changes

VS Code provides an easy way to track your changes. In the image below I have added changes to the current file. VS Code indicates this with a green bar on all the lines that have been added. If existing lines have been modified, this is indicated with a striped blue bar.

<img width="800" alt="Track changes blue striped bar" src="https://github.com/vazevaru/learning-software-engineering.github.io/assets/90367491/421a7b5b-bf66-452f-8cac-04f22664aac0">

Click on the blue bar beside the code to look at the modifications that have been made. If you want to revert back to the changes, press the revert button.

<img width="800" alt="Track changes by section" src="https://github.com/vazevaru/learning-software-engineering.github.io/assets/90367491/711d0053-a7d3-4862-8418-d650dc7b59e9">

You can also look at the changes you've made to the entire file by navigating to the "Source Control" tab on the left pane and clicking on the file.

<img width="800" alt="Track changes whole file" src="https://github.com/vazevaru/learning-software-engineering.github.io/assets/90367491/0fd5d3f9-f99e-41cf-b0c1-fed50ef362d1">

To look at the previous versions of your file, navigate to the "Explorer" tab on the left pane (if that's not the current tab you are on) and then look at "Timeline" at the bottom of the tab.

<img width="369" alt="Timeline" src="https://github.com/vazevaru/learning-software-engineering.github.io/assets/90367491/cf2154ac-05fe-4a9c-8c4c-ee527b250d04">

To revert to a previous version, right click on the file and select "Restore Contents"

<img width="466" alt="Reverting to previous version" src="https://github.com/vazevaru/learning-software-engineering.github.io/assets/90367491/1cca0b99-1e15-49e5-9be5-003c30233066">


### Adding files to be committed

When you're working on a file, VS Code shows you the status of your files. For example, if you create a new file in your repo, the character 'U' appears beside your file as shown indicating that the file is untracked. 

<img width="363" alt="Before staging untracked" src="https://github.com/vazevaru/learning-software-engineering.github.io/assets/90367491/c8483106-9e08-4c2b-a9c5-a16b276d508e">

If you modify a file existing in the git repo, the character 'M' appears beside your file indicating that it has been modified.

<img width="365" alt="After modification before staging" src="https://github.com/vazevaru/learning-software-engineering.github.io/assets/90367491/f1e81f23-e2f5-41aa-990a-c386c93b7e35">

This helps in identifying which files need to be added. To add a file you can navigate to the "Version Control" tab on the left. There you can view the changes you've made and the staged changes. To stage the changes, you can press the "+" button beside the file. Your changes have been successfully staged and ready to be committed!

<img width="367" alt="After modification after staging" src="https://github.com/vazevaru/learning-software-engineering.github.io/assets/90367491/f35c0380-dd4a-417c-8933-0dc126f3d9ec">

If you want to unstage your changes, locate the file under "Staged Changes" and press the "-" button. This will unstage your changes!

<img width="432" alt="Unstage change" src="https://github.com/vazevaru/learning-software-engineering.github.io/assets/90367491/8e7b9147-1fe7-4ee8-9709-a57bf35ab281">


### Committing files

To commit files navigate to the "Version Control" tab. You will see a text box on the top where you can put your commit message.Then press Command + Enter if you're on a Mac or Ctrl + Enter if you're on a Windows machine.

<img width="363" alt="Commit" src="https://github.com/vazevaru/learning-software-engineering.github.io/assets/90367491/d24ac24a-6e0c-4de3-9669-ef0d9a5eda8e">

Your files have now been committed!

To uncommit changes, navigate to the "Version Control" tab and press the "Views and More Actions" button, which is the button with the 3 dots. Hover on the "Commit" option and press "Undo Last Commit". This will uncommit your changes!

<img width="682" alt="Undo last commit" src="https://github.com/vazevaru/learning-software-engineering.github.io/assets/90367491/22adbc5c-1b90-422d-8101-d297a0817337">


### Pushing to GitHub

Once your files are committed and there are no pending files, you can push to GitHub by navigating to the "Version Control" tab and then press "Sync Changes". If you have pending changes, then you may need to commit them before pushing.

<img width="360" alt="Sync Changes" src="https://github.com/vazevaru/learning-software-engineering.github.io/assets/90367491/6ce33bee-46a1-4fc9-88ca-d227d29ed767">

This will push your changes!

### Pulling from GitHub

You can also pull from GitHub using the "Sync Changes" button in the "Version Control" tab as shown above.

You may encounter Merge Conflicts. To resolve merge conflicts in a file, click on the file. You will see all the instances where there are merge conflicts. In the image below, for this conflict, the current change is highlighted in green, whereas the incoming changes are highlighted in blue.

<img width="876" alt="Merge Conflict" src="https://github.com/vazevaru/learning-software-engineering.github.io/assets/90367491/83464456-8ada-4482-8560-4700e1741f51">

Above the Current change section, there are various options available to solve the merge conflict. For example, if you want to accept the current change, click on "Accept Current Change". You can also the "Compare changes" button to compare the changes and edit the current file accordingly to resolve the conflict.

## Closing Remarks

This article only scratches the surface and there is a whole world to explore with Visual Studio Code that could not be fully tapped into in this article. 
To learn more about VS Code, be sure to check out the Additional Resources section for more information. 
Superpowers await you on the other side, what are **you** waiting for?


## Additional Resources

Official Visual Studio Code documentation and user guide: https://code.visualstudio.com/docs

Official Visual Studio Code YouTube channel with numerous playlists: https://www.youtube.com/@code

Learn to code with Visual Studio Code: https://code.visualstudio.com/learn

Visual Studio Code in 100 Seconds: https://www.youtube.com/watch?v=KMxo3T_MTvY

## References and Citations

- All images and videos in this article are generated by the authors unless otherwise stated.
- All information in this article is based on the authors' personal experience and the official Visual Studio Code documentation (links provided as further reading in each section).
  - IntelliSense: (https://code.visualstudio.com/docs/editor/intellisense)
  - Debugging: (https://code.visualstudio.com/docs/editor/debugging)
  - Integrated Terminal: (https://code.visualstudio.com/docs/terminal/basics)
  - Visual Studio Code Tips and Tricks: (https://code.visualstudio.com/docs/getstarted/tips-and-tricks)
  - Visual Studio Code Extensions: (https://code.visualstudio.com/docs/editor/extension-marketplace)
  - Using Git source control in VS Code: (https://code.visualstudio.com/docs/sourcecontrol/overview)
  - Introduction to Git in VS Code: (https://code.visualstudio.com/docs/sourcecontrol/intro-to-git)
  - Getting Started About Version Control: (https://git-scm.com/book/en/v2/Getting-Started-About-Version-Control)
  - Source Control FAQ: (https://code.visualstudio.com/docs/sourcecontrol/faq)

