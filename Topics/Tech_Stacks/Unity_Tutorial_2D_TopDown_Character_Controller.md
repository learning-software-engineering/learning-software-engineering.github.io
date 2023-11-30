# Unity Tutorial: 2D Top-Down Character Controller

## Table of contents
#### [Introduction](#introduction-1) 
#### [Overview](#overview-1) 
#### [Setting Up the Scene](#setting-up-the-scene-1) 
#### [Creating the Player](#creating-the-player-1)
#### [Player Movement](#player-movement-1)
#### [Conclusion](#conclusion-1)


## Introduction
This tutorial will walk you through making a character controller for a top-down 2D game similar to many modern roguelikes such as Vampire Survivors.  
This tutorial assumes you have a basic understanding of how Unity works, and are familiar with Unity's editor UI. Regardless, the tutorial will break the steps down into detail.
If not, then it is highly recommended that you check out the [Unity Basics](https://learning-software-engineering.github.io/Topics/Tech_Stacks/Unity_Intro.html#get-started-with-making-your-first-unity-game){:target="_blank"}  page.  
This tutorial is focused on game mechanics rather than art, so we will be using primitive graphics assets such as squares and circles. Feel free to use your own assets in place of these.  
This tutorial will be using Unity version 2020.3.20f1. Newer LTS (long term support) versions will likely work.
Note that Unity's primary scripting language is C#, so having a basic understanding of it will also assist you in this tutorial. However, all code will be provided.

## Overview
There are two basic and essential components to a character: movement and combat. This tutorial will cover basic physics based movement by setting the player's velocity via WASD inputs. There are other ways to approach 2D movement, such as applying forces to the player, or calculating and updating the player's position directly. There is no one specific best way to do movement, but the one covered in this tutorial is a good place to start as you will get to understand how different parts of unity work. Lets get started!

## Setting Up the Scene
Start by creating a new project. We will use the 2D core preset. Let's name it Top-Down Shooter.  
<img src="https://i.ibb.co/hsMykXw/create-project.png" alt="create-project">  

Once you open the project, you should be greeted with an empty scene. The only thing in your scene should be a gameobject called Main Camera.  
The first we will do is set the background color to whatever color you want. For this tutorial, we will use black.  
To do so, click on the Main Camera object in your heirarchy. Doing so will bring up the gameobject's inspector. The inspector holds information on the different components attached to a gameobject. All gameobjects have a component called Transform (or RectTransform if it is a UI object). The transform component defines various parameters for the object. Namely, its position in space, its rotation, and its scale relative to its default size. Components are what defines what an object is and does. For example, the main camera additionally has a Camera component and an Audio Listener component. The Camera component is what allows our main camera gameobject to function as a camera. This also means that we can add additional, custom functionalities to our gameobjects by creating scripts and attaching them as components. To change the camera's background to black, in the inspector, we will select the Background property in the Camera component and change it to black.  
<img src="https://i.ibb.co/9VN0W72/background-to-black.png" alt="background-to-black">

## Creating the player
Next, we will create a player object. Our player will be a circle. To make the player, right click on empty space in the heirarchy and nagivate to 2D Object -> Sprites -> Circle. This will create a new gameobject with a sprite renderer component attached to it. Name it player (or anything you want).  
<img src="https://i.ibb.co/8XjzXFq/create-player.png" alt="create-player">  
Next, we will add some components to the player. Select the player object via the heirarchy, and in the inspector, click on the Add Component button, which appears beneath all attached components. Search and add Rigidbody2D and CircleCollider2D to the player.  
<img src="https://i.ibb.co/10ngLLN/add-rb-col.png" alt="add-rb-col">  
Unity has a 2D and 3D physics engine. We will be moving the player using said engine. To make an object part of the physics simulation, i.e telling Unity that an object should react to physics, we need to attach a rigidbody to it.
The collider, on the other hand, handles collision, i.e stopping at walls, or getting hit by enemy projectiles.  
In the rigidbody component, change Gravity Scale to 0. This makes it so the player is not affected by gravity. Since our game is a top down shooter, we do not want the player to be dragged downwards by gravity. However, if you are making a platformer, you may choose to set the gravity scale to a positive number.
In the rigidbody component, find the constraints property and check Freeze Rotation Z. This will prevent our player from being rotated as a result of a physical interaction.  
<img src="https://i.ibb.co/1TGKgxH/gravity-0.png" alt="gravity-0">

## Player Movement
Before making the player move, lets add in some walls to the scene. To add a "wall", we will create a square object similar to how we created the player. Right click in the heirarchy and navigate to 2D Object -> Sprites -> Square. Rename the newly created object to "wall". In order for the wall to act as a wall, it must be able to collide with the player, so we will add a BoxCollider2D Component to the newly created wall. To move the wall, we will select the wall in the heirarchy with the Rect Tool selected. Then, in your scene, you can move the wall by clicking and dragging it. You can also reshape it by scaling its x or y scales by clicking and dragging one of its edges or corners. Note that when scaling the wall, its collider will scale with it, so we don't have to reshape the collider. Finally, duplicate the wall a few times and rearrange them to create a simple environment. You may use your creativity, or follow the image below.  
<img src="https://i.ibb.co/nBn50Ws/create-environment.png" alt="create-environment">  
It's finally time to make the player move. We will create a new C# script and attach it to the player. To do so, in the Project tab, first create a Scripts folder under Assets. Inside the Scripts folder, right click and navigate to Create -> C# Script. Name the script PlayerMovement and attach it to the player object by dragging the script over the player object in the heirarchy (there are various ways to attach components to objects, this will be up to you to explore). Open up the script and we will begin coding.

Every script created from the editor will contain a class with the same name as the script. This class extends a class called MonoBehavior, which is essentially Unity's scripting API. Inside this class, you will find two functions; [Start](https://docs.unity3d.com/ScriptReference/MonoBehaviour.Start.html){:target="_blank"}  and [Update](https://docs.unity3d.com/ScriptReference/MonoBehaviour.Update.html){:target="_blank"} . In a nutshell, Start is called once at the start, and Update is called once every frame. Feel free to read the above documentation if you wish to know more. Our goal is to control the player using WASD. We will move the player using its rigidbody. To do so, the script must be able to reference the rigidbody attached to the player. Unity has a very simple way to do this. We can define public class attributes, which the editor can access and assign. We will define a Rigidbody2D variable that holds the player's rigidbody.  
```
public Rigidbody2D rb;
```  
Now, we can do things to the rigidbody. To move the player, we can directly change the player's current velocity. Unity stores a 2D rigidbody's velocity as a [Vector2](https://docs.unity3d.com/ScriptReference/Vector2.html){:target="_blank"} , which is a data type that contains an x and y value. Thus, we need to track the x and y components of the velocity that we want our player to move at. We will declare three new class variables:
```
public float moveSpeed;
float newX;
float newY;
```  
We will use moveSpeed to control how fast the player is moving. We use newX and newY to keep track of the player's current x and y inputs, i.e if the user inputs W, newY = 1, but if the user inputs both W and S at the same time, we may want the player to not move vertically by having newY = 0.
Before that, lets take the user's keyboard inputs. We want to move the player whenever they press WASD. In the update function, write the following code:
```
newX = 0;
newY = 0;
if (Input.GetKey(KeyCode.W)){
    newY += 1;
}
if (Input.GetKey(KeyCode.S)){
    newY -= 1;
}
if (Input.GetKey(KeyCode.A)){
    newX -= 1;
}
if (Input.GetKey(KeyCode.D)){
    newX += 1;
}
```  
At the start of each frame, we reset the newX and newY to 0. In each if condition, we check if a key has been pressed. In each if statement, we modify the respective value to reflect the key inputs.
Next, we can change the rigidbody's velocity attribute using the new x and y values.
``` 
Vector2 newVel = new Vector2(newX, newY);
rb.velocity = newVel.normalized * moveSpeed;
``` 
Vector2.normalized returns the vector with magnitude one. Note that if we did not have this, the player would move faster diagonally. Consider the two vectors (1,0) and (1,1). We get the first vector when the user only presses D, and the second when the user presses W and D. The first vector has magnitude 1, while the second has a magnitude of root2. Thus, the speed resulting from using the second vector will be faster than the first. using .normalized will ensure that the player is moving at the same speed regardless of direction.  
Multiplying newVel with moveSpeed will simply multiply each element in the vector by moveSpeed, similar to multiplying a matrix with a number. By now, your script should be looking like this.  
<img src="https://i.ibb.co/GQsb1Hg/player-movement-script.png" alt="player-movement-script">  
Now, back in the Unity editor. We need to make some changes before the player can move.
First, let's make the camera follow the player. An easy, although limiting, way to do this is by simply making the camera a child of the player. This will make the camera follow the player around. You can do this by dragging the camera object onto the player object in the heirarchy. Next, in the player's inspector, find the PlayerMovement script that we attached earlier. You will see two new fields, RB and MoveSpeed. These are the public class attributes we declared earlier. Remember that RB is supposed to be a reference to the player's rigidbody. We can do this by dragging the player object from the heirarchy into the RB field. When we drag a gameobject into a field, the editor will search through all of its components to see if there are any matching components of the same type as the variable. Finally, change the MoveSpeed field to 5 (or whatever speed you want your player to move at).  
<img src="https://i.ibb.co/J27xsNc/player-script.png" alt="player-script">  
Now, if you play the game in the editor, the player should be moving around via the WASD buttons. Note that in this implementation, the player moves at a constant speed. If you want the player to speed up and slow down, consider looking into the [Rigidbody2D.AddForce](https://docs.unity3d.com/ScriptReference/Rigidbody2D.AddForce.html){:target="_blank"}  function.

## Conclusion
This tutorial covered a very basic implementation of a 2D Top-Down character controller. Movement is often a crucial element of any action game, and has many different implementations fitting for the specific game. For top-down shooters, most games will have some sort of 8 directional or all directional movement either via the mouse, keyboard, or controller. The version implmented in this tutorial is very basic and can be expanded upon. For example, if the game takes place under water or in space, you could simulate inertia, i.e the player slows down to a stop instead of instantly stopping, or you could give the player dashing abilities etc. Unity is well documented and has many online tutorials on topics such as character movement, so it is highly encouraged for you to explore. 