# Introduction to Unity Basics

## Table of contents
#### [Introduction](#introduction)
#### [Download and installation](#download-and-installation)
#### [Create new Unity project](#create-new-unity-project)
#### [Brief intro to Unity interface](#brief-intro-to-the-unity-interface)
#### [Making your First Unity game](#get-started-with-making-your-first-unity-game)
#### [Additional resources](#additional-resources)
#### [References](#reference)

## Introduction 
Unity is a game engine that can be used to develop 2D, 3D, AR/VR games. It can also be used to create interactive simulations for training, education, and various industries. The end product can be built and deployed to mobile, desktop, and web platforms. Unity provides a user-friendly interface for users to design and develop the interface of their projects. The game logic is scripted in C#. Below is a beginner's guide for how to set up and get started with Unity.

## Download and Installation
#### Download Unity Hub
**Unity** Hub is a management tool that can be used to organize Unity projects, install different versions of Unity Editor, manage licenses and access the Unity Asset Store efficiently. It can be used with the Unity Editor version 5.6 or higher.

To get started, download Unity Hub from the [official Unity website](https://unity.com/download). 
Choose the correct installer of Unity Hub for your operating system (Mac, Windows, or Linux).
Open the installer file and follow the instructions in the Unity Hub setup window to install Unity Hub on your machine.

#### License Activation:
An activated license is needed to use Unity. When you sign in to the Unity Hub for the first time, you will be asked to add an active license. 
At the top of Unity Hub, click **Manage licenses**. If you do not see this, you can manage licenses by clicking on the **Preferences (or Settings) icon** on the top of the left tab bar beside your account icon > then select the **license** tab in the window that pops up. 
Click **Add** to add a new license. 
You can choose to get a free personal license or get an educational (student) license by applying for the Unity student plan on [this website](https://unity.com/products/unity-student).
<img width="650" alt="image" src="https://github.com/ruiting-chen/learning-software-engineering.github.io/assets/51133017/ffddd0e9-cc10-451b-9dca-b92edee2c1bd">

#### Install Unity Editor through Unity Hub:
- Open Unity Hub > Navigate to **Installs** on the left taskbar > Select **Install Editor**
- Choose the version of Unity Editor you would like to install. 
  - If you are continuing from an existing Unity project, Unity will prompt you to download the correct version of the Unity Editor associated with that project when you try to open the project.
- When you select the version of Unity Editor to install, you be brought to this page to add modules:
  <img width="650" alt="image" src="https://github.com/ruiting-chen/learning-software-engineering.github.io/assets/51133017/234aaa66-3cc0-4b54-91c3-b9cc2626a8c9">
  
  - In the **Dev Tools** section, you can choose to download the Visual Studio Community if you want to use Visual Studio as your default script editor for C# scripts. If you already have Visual Studio downloaded, or you want to use a different editor to edit the scripts, refer to [Script Editor](#script-editor) section for how to set the default script editor for your Unity Editor. 
  - In the **Platforms** section, choose the appropriate Build support depending on whether you want the end product to be built and deployed as a desktop, mobile, or web application. For example, check the box for "WebGL" if you want to build a web game
  - You can add more modules and download more build supports according to your needs later on. To do so, go to **Installs** in Unity Hub > Click on the **Settings icon** for the version of Unity Editor that you want to modify > Select **Add modules**
    <img width="600" alt="image-1" src="https://github.com/ruiting-chen/learning-software-engineering.github.io/assets/51133017/5810cb89-335a-4386-9272-18263fcb7405">

## Create New Unity Project
Once you have Unity downloaded, you can create a new project by:
- Go into Unity Hub > **Projects** > Select **New Project** in the top right corner.
  - If you are continuing from an **existing** project, go to **Projects** > Select **Add** > Find the folder that contains the Unity Project. Then your project will be opened in Unity (Skip to [Intro to Unity Interface](#brief-intro-to-the-unity-interface) for Unity Interface).
- In the create new project window:
<img width="650" alt="image-2" src="https://github.com/ruiting-chen/learning-software-engineering.github.io/assets/51133017/e0feffb9-d515-4bd0-80cb-18d8c258395d">

  - Select templates to create a 2D, 3D, AR, VR, etc. project according to your need. 
  - On the **top**, you can select the Unity Editor version you want to use
  - On the **right** side, you can specify the project name and location for your project.

## Brief Intro to the Unity Interface
Once you create a new project/open a project in Unity, you will see an interface similar to this. I have split the interface into 5 main sections and will briefly introduce each section. 
<img width="960" alt="Unity_interface" src="https://github.com/ruiting-chen/learning-software-engineering.github.io/assets/51133017/f0c0d37c-ac4b-48ff-a294-2a90b585647b">

1. **Hierarchy window**: 
The hierarchy window displays everything in a **Scene**. In Unity, the things in a Scene, such as the Main Camera, Directional Light, and the SampleObject, are called **GameObjects**. You can use the Hierarchy window to add, delete, group and organize the GameObjects into different levels. 
2. **Scene/Game view**: 
The **scene view** displays the current GameObjects you placed in a scene. You can use the Scene view to manipulate GameObjects and view them from various angles. 
The **game view** displays the rendered view that you will see in the final game product. It's like a "preview" of your game.
You can switch between Scene/Game view in the **top left** corner of this section.
3. **Inspector window**: 
If you click on a GameObject inside the hierarchy window, the inspector window will open on the **right** side of your screen. You will be able to see and edit the properties and components of this GameObject in the Inspector window. 
4. **Project window**: 
The project window acts as a file browser, organizing asset files in folders. An **asset** is a representation of any item that can be used in your game or project, such as images, audio, 3D models, sprites, and texture files. It also contains C# scripts, files, or folders that we create. You can create or import assets and scripts by right-clicking in the project window. Besides the Project window, there is a **Console** window that logs debug information when you run your game.
5. **Toolbar**: 
The toolbar is at the **top** of the Unity Editor. You can press the play/pause button in the middle to run/stop the game in the Game view. The toolbar also contains tabs to access your Unity Account, Unity Cloud Services, and Unity Collaborate. 

Note that you can customize your Unity Interface. You can drag and move the windows to different places and add/remove windows to change the interface appearance according to your preference. Some Unity tutorials that you might find may also have a different appearance of the interface.

#### Script Editor
If you double-click on a script in your Project window, your script will be opened in your default script editor. You will be able to edit the scripts in the editor and see changes reflected in the Unity Editor.

If you have not set the default editor or want to change the default editor, you can:
  - Go to **Edit** in the Toolbar > **Preferences (macOS: Unity > Settings)** to open the Preferences window.
  - Open the External Tools menu.
  - Click on the External Script Editor dropdown and select your preferred default editor or select **Browse** to find your editor. 
  <img width="650" alt="image-3" src="https://github.com/ruiting-chen/learning-software-engineering.github.io/assets/51133017/0243392d-eef1-4ba9-8f24-37ec43b5aa14">

## Get started with making your first Unity game
After you setup and get familiar with the Unity interface, you can start creating your own game in Unity. Here are some resources that could be useful to help you get started: 
- [Get started with 2D Game](https://www.youtube.com/watch?v=ewiw2tcfen8&list=PL0eyrZgxdwhxL5n_wJsnpI4Y9AFIFhhF8): A Youtube video series that provides a step-by-step tutorial from the installation to making a simple 2D game.
- [Get started with 3D Game](https://www.youtube.com/watch?v=n0GQL5JgJcY&list=PLrnPJCHvNZuB5ATsJZLKX3AW4V9XaIV9b): A Youtube series that provides detailed guide for making 3D game in Unity.
- [Learn about making Prefabs in games](https://www.youtube.com/watch?v=OyuyV1Ec7J8&list=PLS57jztVd1_8aoX8ZT6LIyIPQ9JpZriJH&index=1): A beginners Youtube series that introduces Material, Texture, and Prefabs. You can follow this series to make a simple house Prefab in Unity.

## Additional Resources
- [Getting started with the Unity Editor](https://subscription.packtpub.com/book/game-development/9781801078078/2/ch02lvl1sec04/getting-started-with-the-unity-editor): A detailed information page for Unity installation and the Unity interface. 
- [Introduction to Unity fundamentals for absolute beginners](https://www.youtube.com/watch?v=ozL-h75vazQ): A tutorial video for how to place and manipulate objects in the Unity interface.
- [Unity Manual](https://docs.unity3d.com/Manual/index.html): The official Unity website that provides information to different features and aspects that you can learn about in Unity. Note that the manual is slightly different for different versions of Unity.

## Reference
[What is the Unity Hub?](https://support.unity.com/hc/en-us/articles/360061586571-What-is-the-Unity-Hub-#:~:text=The%20Unity%20Hub%20is%20a,and%20installing%20add%2Don%20components.)
[Getting started with the Unity Editor](https://subscription.packtpub.com/book/game-development/9781801078078/2/ch02lvl1sec04/getting-started-with-the-unity-editor)
[Unity Manual](https://docs.unity3d.com/Manual/VisualStudioIntegration.html#:~:text=Unity%20automatically%20uses%20Visual%20Studio,into%20an%20existing%20Unity%20installation.)
[Introduction to Unity Editor and Unity Interface](https://getalow.com/unity-engine/introduction-to-unity-editor-and-unity-interface/16)
 
