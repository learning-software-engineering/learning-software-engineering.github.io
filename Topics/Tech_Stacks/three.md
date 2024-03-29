## Table of Contents
- [Installation](#installation) 
- [Option 1: NPM and build tool](#option-1-for-installation-npm-and-build-tool-recommended-approach)
- [Option 2: Import from CDN](#option-2-for-installation-import-from-a-cdn)
-  [Addons](#addons) 
- [Setting Up Your Files](#setting-up-your-files) 
- [Creating the Scene](#creating-the-scene)
- [Creating and Rendering Your First 3D Object](#creating-and-rendering-your-first-3d-object) 
- [Reasons to Consider Three.js](#reasons-to-consider-threejs) 
- [References](#references)
   
## Installation
<a name="installation"></a>
You will need:
- One html file
- Javascript file with `import * as THREE from 'three';` at the top
- public/ folder. This is also known as a static folder, and will usually contain textures, audio, and 3D models.
  
<a name="option-1"></a>
## Option 1 for installation: NPM and build tool (recommended approach)
1. Install node.js
   We will use this to load and manage dependencies and to run the build tool.
2. Install three.js and a build tool such as Vite through a terminal in your project folder.
   `three.js npm install --save three` Installs three.js.
   `npm install --save-dev vite` Installs Vite. You may use another build tool if you wish.
3. From the terminal, run:
   `npx vite`

Result: You should see a URL such as http://localhost:5173 appear in the terminal, which you can click on to open up the webpage. The page will start off as blank until you create a scene.
When you are ready to deploy your web app, use Vite to run a production build using `npx vite build` in the terminal. Everything used by the app will be copied into the dist/ folder, which will contain everything that can be hosted on your website. 

<a name="option-2"></a>
## Option 2 for installation: Import from a CDN
Installing without build tools will change your project structure.

1. We previously imported code from the npm package 'three' in the javascript file. Web browsers don't understand what that means, so in the html file we will need to add an import
   map defining where to get the package. Put the following code inside the <head></head> tag, after the styles. Replace <version> with an actual version of three.js, a list of which can be found here:
   https://www.npmjs.com/packagethree?activeTab=versions
```html
<script type="importmap">
  {
    "imports": {
      "three": "https://unpkg.com/three@<version>/build/three.module.js",
      "three/addons/": "https://unpkg.com/three@<version>/examples/jsm/"
    }
  }
</script>
```
2. We will also need to run a local server, so the web browser can access these files at a URL. Install Node.js then run the following command in a terminal to start a local server 
   in the project directory.
   `npx serve .`

Result: You should see a URL like http://localhost:3000 appear in your terminal, which you can open to see your web app. This page will start off as blank until you create a scene. When you are ready to deploy your web app, push the source files to your web hosting provider. You will need to keep the import map updated with any dependencies that your app requires. If the CDN hosting your dependencies goes down, your website will go down too.
Importantly, make sure to import all dependencies from the same version of three.js and from the same CDN. Mixing files from different sources may cause duplicate code to be included, or break the application.

<a name="addons"></a>
## Addons:
Certain three.js components, such as controls, loaders, and post-processing effects, are a part of the addons/ directory. Addons need to be imported separately. here is an example of importing some addons:
```javascript
import * as THREE from 'three';
import { OrbitControls } from 'three/addons/controls/OrbitControls.js';
import { GLTFLoader } from 'three/addons/loaders/GLTFLoader.js';

const controls = new OrbitControls( camera, renderer.domElement );
const loader = new GLTFLoader();
```

# Creating Your First Scene and 3D Object with Three.js

This tutorial will guide you through the process of creating your first scene and 3D object using Three.js, a JavaScript library that simplifies the use of WebGL for 3D graphics in a web browser. In order to do this, you'll need: 

-   Basic understanding of HTML, CSS, and JavaScript
-   A browser that supports WebGL
-   Any text / code editor

## Setting Up Your Files

To discuss how to create a functioning scene in Three.js and render your first 3D object, we can examine some code excerpts from the Three.js documentation.

First, you will need to create a new HTML file named `index.html` 

```html
<!DOCTYPE html>  
<html  lang="en">  
	<head>  
		<meta  charset="utf-8">  
		<title>My first three.js app</title>  
		<style> 
			body { margin:  0;  }  
		</style>  
	</head>  
	<body>  
		<script  type="module"  src="/main.js"></script>  
	</body>  
</html>
```

Next, create a JavaScript file `main.js`, make sure to import the Three.js library.

```javascript
// Imports the Three.js library
import  *  as THREE from  'three';  
```

## Creating the Scene

Now that you have your JavaScript file, you'll have to create the scene, camera, and renderer.

```javascript
// Creates the scene and camera
const scene =  new THREE.Scene();  
const camera =  new THREE.PerspectiveCamera(  75, window.innerWidth / window.innerHeight,  0.1,  1000  );  

// Creates the renderer and appends it to the parent HTML document
const renderer =  new THREE.WebGLRenderer(); 
renderer.setSize( window.innerWidth, window.innerHeight ); 
document.body.appendChild( renderer.domElement );
```


- Scene: A scene holds all your objects, cameras, and lights in Three.js.

- Camera: Defines the POV from which you'll see the scene. It contains the attributes (`field of view`, `aspect ratio`, `near`, `far`). In the example, these attributes are set to ( 75, window.innerWidth / window.innerHeight,  0.1,  1000 ) respectively. 

- Renderer: Renders the graphics onto the screen. In the example, the function `renderer.setSize()` sets the size of the renderer to be the same as the display window before `document.body.appendChild()` adds it to the HTML document. 

## Creating and Rendering Your First 3D Object

Now that we have our scene, camera, and renderer, we can get started with creating and animating our first 3D object.

We can do this through the following code excerpt.

```javascript
// Creates a cube and adds it to the scene
var geometry = new THREE.BoxGeometry(1, 1, 1); // Width, Height, Depth
var material = new THREE.MeshBasicMaterial({ color: 0x00ff00 });
var cube = new THREE.Mesh(geometry, material);
scene.add(cube);

// Animates the cube and renders it through the renderer
function animate() {
    requestAnimationFrame(animate);

    // Rotate the cube
    cube.rotation.x += 0.01;
    cube.rotation.y += 0.01;

    renderer.render(scene, camera);
}

animate();` 
```

In order to create a 3D object, in this case a cube, we initialize a `BoxGeometry` with vertices (1, 1, 1). The cube's material, or texture in other words, is set to be `MeshBasicMaterial`, one of the standards that Three.js comes with, and its colour is set to `0x00ff00`. 

We then use `Mesh` to combine the `geometry`, the desired geometrical shape of our object with `material`, the desired texture and colour of our 3D object to create a cube. After which `scene.add()`
adds the initialized cube to the scene we created in the previous section. 

Now, in order to make the cube appear, we create the `animate()` function, which uses `requestAnimationFrame()` to draw the cube onto the scene during every refresh, and `renderer.render()` to actually render the cube.

Additionally, changing `cube.rotation.x` and `cube.rotation.y` on every frame refresh gives the effect of the cube rotating on its x and y axis.

Now all you have to do is open `index.html` in a WebGL-compatible web browser to see your scene. You should see a rotating green cube against a black background.

You can view an live example of the finished product through this [link](https://jsfiddle.net/0c1oqf38/) provided in the Three.js documentation.

## Reasons to consider Three.js

Three.js is a simple yet powerful tool that makes creating 3D graphics on the web easy and accessible. It allows people to build and manipulate 3D scenes without extensive knowledge of WebGL, which is complex and can be very daunting for many beginners. This makes it a very valuable tool that opens up many opportunities for anyone that is considering venturing into the world of 3D design and web development. 

You can also view what others have done with Three.js on the library's [website](https://threejs.org).

## References
- https://threejs.org/docs/#manual/en/introduction/Installation
- https://threejs.org/docs/#manual/en/introduction/Creating-a-scene
- https://threejs.org

