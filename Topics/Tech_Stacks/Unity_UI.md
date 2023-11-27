# A Beginner's Guide for Unity UI Design

### Table of contents
#### [Introduction](#introduction)
#### [Start with Canvas](#start-with-canvas)
#### [Add UI element](#add-ui-element)
#### [Hierarchy: Order of UI element](#hierarchy-order-of-ui-element)
#### [Customize your UI element!](#customize-your-ui-element)
#### [How fancy the Unity UI can be](#how-fancy-the-unity-ui-can-be)
#### [Additional resources](#additional-resources)
#### [References](#references)

## Introduction

Unity is one of the most powerful tool for game development while the User Interface (UI) 
provides the most direct way to interact and guide users. Unity has its own Uinity UI system that allows game developers to create dynamic and interactive User Interface design while can also integrate into the game fast and quick.

Here is a guidance for beginners to start designing their UI in Unity. For more details, please go and check the official [Unity Documentations](https://docs.unity3d.com/2023.3/Documentation/Manual/UIToolkits.html) for the version that you use.

> Here we assume you already have know the basics of Unity and we will not introduce how to make the game in Unity scenes here.
> Please checkout [Introduction to Unity Basics](Unity_Intro.md) section if you are not familiar with the basics!

## Start with Canvas

The Canvas is the place where you create and design your UI. It is independent from the actually game scene design and all other Game Objects, and you will find it always on top your other 3D objects or 2D sprite in the game scene. However, what is cool about Unity UI is that you can connect the UI with the actually game through game logic scripts.

![Screenshot 2023-11-25 at 10 10 51 PM](https://github.com/arielchen07/learning-software-engineering.github.io/assets/105243552/af7b47a8-175d-4008-bc91-ddda181198ee)
> Here is an example of how the Canvas looks like relative to other Game Objects in scene view. The plane with *New Text* on it is the Canvas and the tiny cube in the button left corner is a Game Object. Notice that the relative size of the Canvas and Game Objects shown here is not the actually appearance in the game. You should switch to the Game view to see its layout in the actual game.

The Canvas is a Game Object with a Canvas component on it. All the UI element that you created later will be the children of a Canvas.

The Canvas will not be created when you create a new project in Unity, however you can create it by either of the following:
1. right click anywhere in the hierarchy and select **UI > Canvas**
2. directly create your first UI element and the Canvas will be automatically created along the way

![Screenshot 2023-11-23 at 10 41 24 PM](https://github.com/arielchen07/learning-software-engineering.github.io/assets/105243552/89523047-c4bc-4cf5-af52-ef8d4fec8b67)

> Tip: If you find the Canvas is not facing towards you, click on the direction arrows on the orientation tool bar to modify the Canvas facing angle.
<img width="105" alt="Screenshot 2023-11-23 at 7 06 55 PM" src="https://github.com/arielchen07/learning-software-engineering.github.io/assets/105243552/db1220d1-d0ff-4516-a407-50ad58ad9cbc">

## Add UI element

UI elements will be created as the children of the Canvas Game Object.

To create a new UI element, click on the menu **GameObject** or right click anywhere in the hierarchy, hover to **UI** and choose the type of element you want. 

![Screenshot 2023-11-23 at 10 47 23 PM](https://github.com/arielchen07/learning-software-engineering.github.io/assets/105243552/9df58333-1d4c-4462-beda-23d9bed33d89)

Here, we take Text Game Object as an example. By choosing **Text > TextMeshPro**, you should have a new Text Game Object created in the left-side panel of Hierarchy.  

You can create many other types of Game Objects in the simialr fashion.

## Hierarchy: Order of UI element

You probably feel confused when first see Hierarchy in the last section. What is Hierarchy?

In Unity UI, all UI elements will be draw to the Canvas in the same order as they appeared under Canvas Game Object in Hierarvhy window. In other words, if two Game Objects have some overlap, then the latter obejct will be on the top as it will be drawn later.

![Screenshot 2023-11-23 at 12 06 47 AM](https://github.com/arielchen07/learning-software-engineering.github.io/assets/105243552/966981f3-0d0b-48cb-8ac2-56ed2e28ed22)

You can change the order of Game Object by simply dragging them in the Hierarchy window.

## Customize your UI element!

At this point, you should know how to create different kinds of UI element on the Canvas. Now it is the time to design them with your unique style!

Here are some basics tools that you might need during the design.

### The Rect Tool
On the top left of the toolbar, you will find some rect tools that can help you manupulate your UI element.

![GUI_Rect_Tool_Button](https://github.com/arielchen07/learning-software-engineering.github.io/assets/105243552/c0f7e468-d19f-43ee-9ba4-5f31230f9fb4)

With that said, you can move, resize and rotate UI elements once you select the UI element. You can move the UI element by clicking somewhere inside the element and dragging it tp the place you want. You can resize it by clicking on the edges or corners and dragging. The element can be rotated by hovering the cursor slightly away from the corners until the mouse cursor looks like a rotation symbol. You can then click and drag in either direction to rotate.

### Inspector

If you double clicked the UI element in the Hierarchy window, you should have the Inspector window shown on your right. All the properties and components of the UI element should be editable in the Inspector window.

<img width="343" alt="Screenshot 2023-11-23 at 6 42 01 PM" src="https://github.com/arielchen07/learning-software-engineering.github.io/assets/105243552/f64fe1d8-c602-4d20-ba19-f6a5085ffe8d">

Most of the components are intuitive to understand and easy to modify, so here we will introduce one of the most important components for all Game Objects:

### Rect Transform
Rect Transform helps modify the position, rotation, and scale of the Game Object, while it also has a width and height attribute that can decide the dimensions of the UI element.

**Pivot** and **Anchor** are two useful concept to understand here. 

**Pivot**: Pivot is a small circle on the UI element. All the modifications like rotation, size, and scale, will based on the position of the pivot. You can try different positions of pivot to see how it affects the outcome of a rotation, resizing, or scaling. 

**Anchor**: Anchors are shown as four small triangular in the Scene View. The anchoring allows the child to stretch together with the width or height of the parent. Each corner of the rectangle has a fixed offset to its corresponding anchor. This way the different corners of the rectangle can be anchored to different points in the parent rectangle. You can also think of Anchor as setting relative position to the parent object.

<img width="410" alt="285633157-d28a65b3-4864-4201-83f0-097dfe88a5e3" src="https://github.com/arielchen07/learning-software-engineering.github.io/assets/105243552/e298bda2-cf2a-4330-94c5-417038e178fb">

![UI_Anchored1](https://github.com/arielchen07/learning-software-engineering.github.io/assets/105243552/a23fe607-1f14-49e8-b2a1-6091d0dc4e7e)
![UI_Anchored2](https://github.com/arielchen07/learning-software-engineering.github.io/assets/105243552/79bea6bf-2cd1-47d4-969c-e42ebe96e1bc)

> Here are two cases of how pivot and anchor functioning.

## How fancy the Unity UI can be

Now, you should have some basic understandings of Unity UI. But what makes Unity UI so different is that it supports many fancy functionalities that other UIs don't have.

1. UI Animation: WIth Unity UI Animation System, UI elements properties, such as position, scale, or color, can be modified over time. Check out the video [Master UI ANIMATIONS!](https://www.youtube.com/watch?v=YqMpVCPX2ls&list=PL1aAeF6bPTB5N-_01xjNIOg9_refqTxVv&index=16) for more vivid demonstrations.

2. Integration with Game Development: As we mentioned above, you can attach C# scripts to UI elements! This enable the UI to respond to user input and integrate with the overall game logic.  
The most common example would be to attach a script for button UI element. [Button Click Events Unity C#](https://www.youtube.com/watch?v=woPW2_vuSXw)

3. 3D objects on the Canvas: Another cool thing that Unity UI can achieve to to place 3D object onto the Canvas. Here is a quick tutorial for how to make this happend! [Placing 3D objects on a Unity canvas](https://www.youtube.com/watch?v=8yzpjkoE0YA)

## Additional resources
[Unity Documentation](https://docs.unity3d.com/2023.3/Documentation/Manual/UIToolkits.html): You definitely checkout official documentation of Unity UI for usage!  
[Unity UI Manual](https://docs.unity3d.com/Packages/com.unity.ugui@2.0/manual/index.html): This is the specific section of Unity UI that contains more details.  
[Get started with Unity UI (GUI system)](https://www.youtube.com/watch?v=xmR07iBW7zk&list=PL1aAeF6bPTB5N-_01xjNIOg9_refqTxVv&index=1): A series of tutorials that introduce Unity UI in great details!  
[The Unity Tutorial For Complete Beginners](https://www.youtube.com/watch?v=XtQMytORBmM): A hands-on tutorial for making a Flappy Bird game!  
[How To Get A Better Grid Layout in Unity](https://www.youtube.com/watch?v=CGsEJToeXmA&list=RDCMUCR35rzd4LLomtQout93gi0w&index=2): Organize your UI structurally  
[Optimization Tips For Unity UI](https://unity.com/how-to/unity-ui-optimization-tips): How to make the most out of the Unity UI 
