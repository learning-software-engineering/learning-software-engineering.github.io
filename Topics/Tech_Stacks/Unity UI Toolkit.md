# Introduction to Unity UI Toolkit

## Table of Contents
#### [Introduction](#introduction-1)
#### [Get Started](#get-started-1)
#### [UI Toolkit vs. Unity UI](#ui-toolkit-vs-unity-ui-1)
#### [Additional Resources](#additional-resources-1)

## Introduction <a id="introduction-1"></a>

UI Toolkit is a collection of features, resources and tools for developing user interface(UI) in Unity. It offers toolkit to build not only UI for games and applications, but also extentions for Unity Editor and debugging tools.

This tutorial assumes basic understanding of Unity(see [Introduction to Unity Basics](/Unity_Intro.md)), and some intuition about Unity UI(see [A Beginner's Guide for Unity UI Design](/Unity_UI.md))

In this tutorial, we will explain some basics of UI Toolkit, make sure you make the right choice between Unity UI and UI Toolkit for your next Unity project.


## Get Started <a id="get-started-1"></a>

Here we have a project completely fresh, the editor version is 2022.3.18f1 for your reference.

Now we create a UIDocument object in the scene. Like a Canvas object in Unity UI, a UIDocument is what the scene refers to as a placeholder for UI that is going to be displayed on the screen.

![Created UIDocument in Scene](Unity%20UI%20Toolkit/Created%20UIDocument%20in%20Scene.png)

Then create a UIDocument in the assets folder. Despite the same name, this is the source asset, which is the actual contents of the UI.

![Created UIDocument in Assets](Unity%20UI%20Toolkit/Created%20UIDocument%20in%20Assets.png)

Remember to drag your UI contents into its placeholder in the inspectore. This will link them together so that the editor knows which UI to display in this scene.

![Select Source Asset](Unity%20UI%20Toolkit/Select%20Source%20Asset.png)

Double-click the UI contents in the assets folder. This is the UI Builder interface, where the entire interface is dedicated to adjust the details of the UI.

![UI Builder](Unity%20UI%20Toolkit/UI%20Builder.png)

If you want to know more about using UI Toolkit, see [Unity UI Toolkit Beginner's Guide](https://www.youtube.com/watch?v=0mYtI21Fmg4&list=PLgCVPIIZ3xL_FVLhDrC3atsy8CiZzAMh6) if you want to learn it thoroughly, or [Unity UI Toolkit in 5 Minutes](https://www.youtube.com/watch?v=yUXFHAOXhcA) if you already had much experience with Unity.

## UI Toolkit vs. Unity UI <a id="ui-toolkit-vs-unity-ui-1"></a>

So if you want to make your next Unity project, which option is the best?

- If you want to make UI that is not just on the user's screen, choose Unity UI. For example, if you want to make a TV in game that broadcasts information on its screen, this is World Space UI, which can only be implemented by Unity UI exclusively.

- If you are more familiar with the skillset of web development, chooose UI Toolkit. In UI Toolkit, you can style your UI with a Unity Style Sheet(USS), which is inspired by Cascading Style Sheets(CSS) from HTML. With the help of style sheets, you can easily style your UI in a fast and efficient way.

These two criteria are some problems that new Unity users might encounter, see [Comparison of UI systems in Unity](https://docs.unity3d.com/Manual/UI-system-compare.html) for more in depth comparisons.

## Additional Resources <a id="additional-resources-1"></a>

- [What about UI Toolkit?](https://www.youtube.com/watch?v=Wz3k6afpDv8) This video talks about the comparisons so far and the potential for UI toolkit.
- [My disappointment with Unity's UI Toolkit](https://mortoray.com/my-disappointment-with-unity-uitoolkit/) This article talks about the frustrations and limitations of UI Toolkit.
- [Unity UI Toolkit is better than expected](https://prographers.com/blog/unity-ui-toolkit-is-better-than-expected) This article talks about some coding benefits of UI Toolkit.
- [Can anyone do an ELI5 for what is going on with uGUI vs UI Toolkit and the documentation?](https://www.reddit.com/r/Unity3D/comments/13agbid/can_anyone_do_an_eli5_for_what_is_going_on_with/) This reddit post has some interesting discussion over the comparisons between Unity UI and UI Toolkit.