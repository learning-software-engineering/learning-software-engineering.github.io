# Intro to Godot

## What is Godot?
![Godot Game Engine.png](02-3d-outdoor-with-editor.png)
Godot is an open source game engine which is considered a versatile platform for developing 2D as well as 3D games to release on the web, mobile, desktop and even console![^1]

It was originally developed in 2001 by an Argentinian Game Studio. Ever since it got released as an open source game engine, the features it provide has tremendously improved.

Some games one might recognize that are made by the Godot game engine includes would be games like Dome Keeper as well as Endoparasitic.

## Features

The features it includes are:
- Code Editor
- Animation Editor
- Debugger
- Tilemap Editor and More
- It supports Blender
- It supports C# programming
- It also has a custom programming language called GDScript which is similar to python in terms of syntax
- Asset Library is a platform where users can upload and download pre-made assets for their game development
![Godot Asset Library](Godot-intro-2.jpg)

## How to Get Started
### Installation
1. Go to the Godot [official website](https://godotengine.org/) and download the engine. (For linux users go to this [website](https://godotengine.org/download/linux/))
	- There's 2 types of engine, one is the latest version and the other one is the Long Term Support (LTS) version
	- I will be using the Latest Version (4.2.1) for this intro.
2. Unzip the folder and open `Godot_v4.2.1-stable_win64.exe`
### Starting a new Project
After opening the game engine, you'll see something like this:
![Godot Project Menu](Godot-intro-1.jpg)
To create a new project you'll have to:
1. Click on `New`
2. Create a folder to store your project or find a path to the directory you want to store the project
	- Note: Creating a project will not create a new directory, it'll simply put all the required files within the path you set it to
3. Create and your done!
### Introduction to the UI of the Game Engine
![Godot Project View](Godot-intro-3.jpg)
Here's a breif introduction to the interface and what you could do with it.
1. The Scene [^2]
   - This is where you create Nodes.
   	- Nodes are basically building blocks for a game, they could be either moving mobs, objects or even traps that the player node can interact with.
   	- They have names, editable attributes, can be extended and have a callback attribute every frame
   - The scene is basically a group of nodes that makes up a stage for your game
        - It always consist of one parent node, and running a game means running a scene. A game can consist of many scenes but for a game to run, they'll have to run on one of the scenes.
2. File System [^3]
     - This is where all your scripts, images, models, audio and many other file component of your project are stored.
3. 
## References
[^1]: [Introduction to Godot](https://docs.godotengine.org/en/stable/getting_started/introduction/introduction_to_godot.html)
[^2]: [Scenes and Nodes](https://docs.godotengine.org/en/3.1/getting_started/step_by_step/scenes_and_nodes.html#scenes)
[^3]: [File System](https://docs.godotengine.org/en/stable/getting_started/introduction/first_look_at_the_editor.html#:~:text=There%20are%20four%20main%20screen,design%20levels%20for%203D%20games.)