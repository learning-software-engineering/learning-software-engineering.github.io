# Unity

Unity is a game engine that can be used to develop 2D, 3D, AR/VR games. It can also be used to create interactive simulations for training, education, and various industries. The end product can be built and deployed to mobile, desktop, and web platforms. Unity provides a user-friendly interface for users to design and develop the interface of their projects. The game logic is scripted in C#. Below is a beginner's guide for how to set up and get started with Unity.

## Table of contents
### [Introduction](#introduction-1)
### [Why use TypeScript](#why-use-typescript-1)
### [How to use TypeScript](#how-to-use-typescript-1)
### [Additional Resources](#additional-resources-1)

## Download and Installation
#### Download Unity Hub
Unity Hub is a management tool that can be used to organize Unity projects, install different versions of Unity Editor, manage licensing and access the Unity Asset Store efficiently. It can be used with the Unity Editor versions 5.6 or higher.

To get started, download Unity Hub from the [official Unity website](https://unity.com/download). 
Choose the correct installer of Unity Hub for your operating system (Mac, Windows, or Linux).
Open the installer file and follow the instructions in the Unity Hub setup window to install Unity Hub on your machine.

#### License Activation:
An activated license is needed to use Unity. When you sign in into the Unity Hub for the first time, you will be asked to add an active license. 
At the top of Unity Hub, click "Manage licenses". If you do not see this, you can manage licenses by clicking on the preferences (or settings) icon on the top of the left tab bar beside your account icon > then select the liscense tab in the window that pop up. 
Click "Add" to add a new license. You can choose to get a free personal license or get a educational (student) license by applying for Unity student plan on [this website](https://unity.com/products/unity-student).

You need a Unity 
What is Unity License?
Do you need Unity License to develope Unity projects?
How to setup?

#### Install Unity Editor through Unity Hub:
- Open Unity Hub > Nevigate to "Installs" on the left task bar > Select "Install Editor"
- Choose the version of Unity Editor you would like to install. 
  - If you are continuing from an existing Unity project, Unity will prompt you to download the correct version of the Unity Editor associated with that project when you try to open the project.
- When you selected the version of Unity Editor to install, you be brought to this page to add modules:
![Alt text](image.png)
  - In the "Dev Tools" section, you can choose to download the Visual Studio Community if you want to use Visual Studio as your default script editor for C# scripts. If you already have Visual Studio downloaded, or you wanted to use a different editor to edit the scripts, refer to ____ section for how to set default script editor for your Unity Editor. 
  - In the "Platforms" section, choose the appropriate Build support depending on whether you want the end product to be build and deployed as a desktop, mobile, or web application. For example, check the box for "WebGL" if you want to build a web game
  - You can add more modules and download more build supports according to your need later on. To do so, go to "Installs" in Unity Hub > Click on the settings logo for the version of Unity Editor that you want to modify> Select "Add modules"
![Alt text](image-1.png)

## Create New Unity Project
Once you have Unity downloaded, you can create a new project by:
- Go into Unity Hub > Porjects > Select "New Project" on the top right corner.
  - If you are continuing from an existing project, go to Porjects > Select "Add" > Find the folder that contains the Unity Project. Then your project will be opened in Unity (Skip to _____ for Unity Interface).
- In the create new project window:
![Alt text](image-2.png)
  - Select templates to create a 2D, 3D, AR, VR, etc. project according to your need. 
  - On the top, you can select the Unity Editor version you want to use
  - On the right side, you can specify project name and location for your project.

## Brief Intro to the Unity Interface
Once you created a new project/opened a project in Unity, you will see a interface similar to this. I have split the interface into 5 main sections and will breifly introduce each section.

1. Hierarchy window: 
The hierarchy window displays everything in a **Scene**. In Unity, the things in a Scene, such as Main Camera, Directional Light, and the SampleObject, are called **GameObjects**. You can use the Hierarchy window to add, delete, group and organize the GameObjects into different levels. 
2. Scene/Game view: 
The scene view displays the current GameObjects you placed in a scene. You can use the Scene view to manipulate GameObjects and view them from various angles. 
The game view displays the rendered view that you will see in the final game product. It's like a "preview" of your game.
You can switch between Scene/Game view on the top left corner of this section.
3. Inspector window: 
If you click on a GameObject inside the hierarchy window, you will be able to see and edit the properties and components of this GameObject in the Inspector window. 
4. Project window: 
The project window acts as a file browser, organizing asset files in folders. An asset is a representation of any item that can be used in your game or project, such as images, audio, 3D models, sprites, and texture files. It also contains C# scripts, files, or folders that we create. You can create or import assets and scripts by right-clicking in the project window. Beside the Project window, there is a Console window that log debug information when you run your game.
5. Toolbar: 
The toolbar is at the top of the Unity Editor. You can press the play/pause button in the middle to run/stop the game in Game view. The toolbar also contains tabs to access your Unity Account, Unity Cloud Services, and Unity Collaborate. 

#### Script Editor
If you double click on a script in your Project window, your script will be opened in your default script editor. You will be able to edit the scripts in the editor and see changes reflected in the Unity Editor.

If you have not set the default editor or want to change the default editor, you can:
  - Go to Edit in the Toolbar > Preferences (macOS: Unity > Settings) to open the Preferences window.
  - Open the External Tools menu.
  - Click on the External Script Editor dropdown and select your preferred default editor or select "Browse" to find you editor. 
![Alt text](image-3.png)


## Additional Resources

- [This website](https://subscription.packtpub.com/book/game-development/9781801078078/2/ch02lvl1sec04/getting-started-with-the-unity-editor) provides detailed information for getting started with Unity. 
- The first 2 videos of [this Youtube series](https://www.youtube.com/watch?v=ewiw2tcfen8&list=PL0eyrZgxdwhxL5n_wJsnpI4Y9AFIFhhF8) also provides tutorial for install and setup Unity, and introduction to the Unity interface.
- To learn more about Unity in depth, you can watch ____

## Reference
https://support.unity.com/hc/en-us/articles/360061586571-What-is-the-Unity-Hub-#:~:text=The%20Unity%20Hub%20is%20a,and%20installing%20add%2Don%20components.
https://subscription.packtpub.com/book/game-development/9781801078078/2/ch02lvl1sec04/getting-started-with-the-unity-editor
https://docs.unity3d.com/Manual/VisualStudioIntegration.html#:~:text=Unity%20automatically%20uses%20Visual%20Studio,into%20an%20existing%20Unity%20installation.
https://docs.unity3d.com/Manual/system-requirements.html (unused)
https://getalow.com/unity-engine/introduction-to-unity-editor-and-unity-interface/16
 